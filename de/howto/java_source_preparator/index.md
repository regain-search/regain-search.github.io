---
title: "How-To: Präparator für Java-Quellcode"
---

[English translation](/en/howto/java_source_preparator/)

How-To: Präparator für Java-Quellcode
=====================================

**Das Zusatzfeature:**

Parsen von Java-Quellcode ermöglichen und damit Java-Quellcode über regain durchsuchbar machen.

**Lösungsansatz:**

Einen neuen [Präparator](/de/components/preparator/) implementieren.

**Vorteile:**

  * Java-Quellcode muss nicht mit dem `PlainTextPreparator` geparsed werden. Der Quellcode ist nicht als einfacher Text im Index, sondern in aufbereiteter Form.
  * Die Suche mit regain ist schneller als eine JAVA-IDE-Suche.

**Nachteile:**

  * Benötigt große Teile der Eclipse IDE und ist dadurch schwergewichter als eigentlich nötig. D.h. es wird viel ungenutzter Code mitgeschleppt, so dass der Präparator 13 MB groß ist.

**Autor:**

Thomas Tesche (thtesche), cluster:Systems CSG GmbH, http://www.clustersystems.info/


Download
--------

**Binaries:**

Man benötigt einen großen Teil einer Eclipse 3.3 Distribution. Da die verwendeten Klassen innerhalb der Distribution immer wieder verschoben werden, muss man die Abhängkeiten der aktuell verwendeten Distri berücksichtigen. Aus einer Eclipse 3.3.1 Distri wurden folgende jar's verwendet:

  * `org.eclipse.core.contenttype_3.2.100.v20070319.jar`
  * `org.eclipse.core.jobs_3.3.1.R33x_v20070709.jar`
  * `org.eclipse.core.resources_3.3.1.R33x_v20080205.jar`
  * `org.eclipse.core.runtime_3.3.100.v20070530.jar`
  * `org.eclipse.equinox.common_3.3.0.v20070426.jar`
  * `org.eclipse.equinox.preferences_3.2.101.R33x_v20080117.jar`
  * `org.eclipse.jdt.core_3.3.3.v_793_R33x.jar`
  * `org.eclipse.osgi_3.3.2.R33x_v20080105.jar`

**Download des fertigen Präparators:**

Enthalten in der regain Standardversion.


Anleitung
---------

Klasse `JavaPreparator`:

```java
package net.sf.regain.crawler.preparator;

import net.sf.regain.crawler.preparator.java.*;
import java.util.ArrayList;
import java.util.Vector;
import net.sf.regain.RegainException;
import net.sf.regain.crawler.document.AbstractPreparator;
import net.sf.regain.crawler.document.RawDocument;

public class JavaPreparator extends AbstractPreparator {

  public JavaPreparator() throws RegainException {
    super(new String[]{"text/java"});
  }

  public void prepare(RawDocument rawDocument) throws RegainException {
    Vector<String> contentParts = new Vector<String>();
    Vector<String> titleParts = new Vector<String>();

    try {
      // Creates the parser
      JavaParser parser = new JavaParser();
      parser.setSource(rawDocument.getContentAsString());
      JClass cls = parser.getDeclaredClass();

      String class_interface = cls.isInterface() ? "Interface: " : "Class: ";

      titleParts.add(class_interface + cls.getClassName());
      // extract the class info (including inner classes)
      contentParts.add(extractClassInfo(cls, false).toString());

      setTitle(concatenateStringParts(titleParts, Integer.MAX_VALUE));
      setCleanedContent(concatenateStringParts(contentParts, Integer.MAX_VALUE));
    } catch (Exception ex) {
      throw new RegainException("Error parsing Java file: " + rawDocument.getUrl(), ex);
    }
  }

  private StringBuffer extractClassInfo(JClass cls, boolean innerClass) {
    StringBuffer strBuffer = new StringBuffer();

    //For each class add Class Name field
    String class_interface = "";
    if (cls.isInterface()) {
      class_interface = " Interface: ";
    } else if (innerClass) {
      class_interface = ", InnerClass: ";
    } else {
      class_interface = " Class: ";
    }

    strBuffer.append(class_interface).append(cls.getClassName());

    String superCls = cls.getSuperClass();
    if (superCls != null) //Add the class it extends as extends field
    {
      strBuffer.append(", Superclass: ").append(superCls);
    }

    // Add interfaces it implements
    ArrayList interfaces = cls.getInterfaces();
    for (int i = 0; i < interfaces.size(); i++) {
      strBuffer.append(", implements: ").append((String) interfaces.get(i));
    }

    // Add details  on methods declared
    strBuffer.append(extractMethodInfo(cls));

    // Examine inner classes and extract the same details as for the class
    ArrayList innerCls = cls.getInnerClasses();
    for (int i = 0; i < innerCls.size(); i++) {
      strBuffer.append(extractClassInfo((JClass) innerCls.get(i), true));
    }

    return strBuffer;
  }

  private StringBuffer extractMethodInfo(JClass cls) {
    StringBuffer strBuffer = new StringBuffer();

    // get all methods
    ArrayList methods = cls.getMethodDeclarations();
    for (int i = 0; i < methods.size(); i++) {
      JMethod method = (JMethod) methods.get(i);

      strBuffer.append(", ");
      // Add return type field
      String returnType = method.getReturnType();
      if (returnType != null) {
        if (!returnType.equalsIgnoreCase("void")) {
          strBuffer.append(" ").append(returnType);
        }
      }

      // Add method name field
      strBuffer.append(" ").append(method.getMethodName()).append("(");

      ArrayList params = method.getParameters();
      for (int k = 0; k < params.size(); k++) // For each method add parameter types
      {
        if (k != 0) {
          strBuffer.append(" ");
        }
        strBuffer.append((String) params.get(k));
      }
      strBuffer.append(") ");

      String code = method.getCodeBlock();
      if (code != null) //add the method code block
      {
        strBuffer.append(code);
      }
    }

    return strBuffer;
  }

  private StringBuffer extractImportDeclarations(JavaParser parser) {
    StringBuffer strBuffer = new StringBuffer();

    ArrayList imports = parser.getImportDeclarations();
    if (imports == null) {
      return strBuffer;
    }

    for (int i = 0; i < imports.size(); i++) //add import declarations as keyword
    {
      strBuffer.append((String) imports.get(i));
    }

    return strBuffer;
  }

  private StringBuffer extractComments(JavaParser parser) {
    StringBuffer strBuffer = new StringBuffer();
    ArrayList comments = parser.getComments();
    if (comments == null) {
      return strBuffer;
    }

    for (int i = 0; i < comments.size(); i++) {
      String docComment = (String) comments.get(i);
      strBuffer.append(docComment);
    }

    return strBuffer;
  }

}
```


Klasse `JavaParser.java`:

```java
package net.sf.regain.crawler.preparator.java;

import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;
import net.sf.regain.RegainException;
import org.eclipse.jdt.core.dom.*;

public class JavaParser {
  private ASTParser _parser = ASTParser.newParser(AST.JLS3);
  private CompilationUnit _unit = null;
  private JClass _class = null;

  public void setSource(String sourceStr) throws RegainException {
    try {
      _parser.setKind(ASTParser.K_COMPILATION_UNIT);
      _parser.setSource(sourceStr.toString().toCharArray());
      _unit = (CompilationUnit) _parser.createAST(null);
    } catch (Exception ex) {
      throw new RegainException("Error parsing Java file", ex);
    }
  }

  public ArrayList getImportDeclarations() {
    List imports = _unit.imports();
    if (imports.size() == 0) {
      return null;
    }

    ArrayList importDecl = new ArrayList();
    ListIterator iter = imports.listIterator();
    while (iter.hasNext()) {
      ImportDeclaration decl = (ImportDeclaration) iter.next();
      importDecl.add(decl.getName().toString());
    }

    return importDecl;
  }

  public ArrayList getComments() {
    List comments = _unit.getCommentList();
    if (comments.size() == 0) {
      return null;
    }

    ArrayList javaDocComments = new ArrayList();
    ListIterator iterator = comments.listIterator();
    while (iterator.hasNext()) {
      Object object = iterator.next();
      if (object instanceof Javadoc) {
        String comment = ((Javadoc) object).getComment();

        javaDocComments.add(comment);
      }
    }

    return javaDocComments;
  }

  public JClass getDeclaredClass() {
    List types = _unit.types();
    ListIterator typeIter = types.listIterator(0);
    if (typeIter.hasNext()) {
      TypeDeclaration object = (TypeDeclaration) typeIter.next();
      _class = new JClass();
      setClassInformation(_class, object);
      return _class;
    }
    return null;
  }

  private void setClassInformation(JClass cls, TypeDeclaration object) {
    cls.setIsInterface(object.isInterface());
    cls.setClassName(object.getName().getIdentifier());

    SimpleType _superClass = (SimpleType) object.getSuperclassType();
    if (_superClass != null) {
      cls.setSuperClass(_superClass.getName().getFullyQualifiedName());
    }

    List interfaceLst = object.superInterfaceTypes();

    ListIterator interfaces = interfaceLst.listIterator();
    while (interfaces.hasNext()) {
      SimpleType sin = (SimpleType) interfaces.next();
      cls.getInterfaces().add(sin.toString());
    }

    addMethods(cls, object);

    TypeDeclaration[] innerTypes = object.getTypes();
    for (int i = 0; i < innerTypes.length; i++) {
      JClass innerCls = new JClass();
      setClassInformation(innerCls, innerTypes[i]);
      cls.getInnerClasses().add(innerCls);
    }
  }

  private void addMethods(JClass cls, TypeDeclaration object) {
    MethodDeclaration[] met = object.getMethods();
    for (int i = 0; i < met.length; i++) {
      MethodDeclaration dec = met[i];
      JMethod method = new JMethod();
      method.setMethodName(dec.getName().toString());
      Type returnType = dec.getReturnType2();
      if (returnType != null) {
        method.setReturnType(returnType.toString());
      }
      Block d = dec.getBody();
      if (d == null) {
        continue;
      }
      method.setCodeBlock(d.toString());
      List param = dec.parameters();
      ListIterator paramList = param.listIterator();
      while (paramList.hasNext()) {
        SingleVariableDeclaration sin = (SingleVariableDeclaration) paramList.next();
        method.getParameters().add(sin.getType().toString());
      }
      cls.getMethodDeclarations().add(method);
    }
  } 
}
```
 

Klasse `JClass.java`:

```java
package net.sf.regain.crawler.preparator.java;

import java.util.ArrayList;

public class JClass {
  private String className = null;
  private boolean isInterface = false;
  private ArrayList methodDeclarations = new ArrayList();
  private ArrayList innerClasses = new ArrayList();
  private String superClass = null;
  private ArrayList interfaces = new ArrayList();

  public String getClassName() {
    return className;
  }

  public void setClassName(String className) {
    this.className = className;
  }

  public boolean isInterface() {
    return isInterface;
  }

  public void setIsInterface(boolean isInterface) {
    this.isInterface = isInterface;
  }

  public ArrayList getMethodDeclarations() {
    return methodDeclarations;
  }

  public void setMethodDeclarations(ArrayList methodDeclarations) {
    this.methodDeclarations = methodDeclarations;
  }

  public ArrayList getInnerClasses() {
    return innerClasses;
  }

  public void setInnerClasses(ArrayList innerClasses) {
    this.innerClasses = innerClasses;
  }

  public String getSuperClass() {
    return superClass;
  }

  public void setSuperClass(String superClass) {
    this.superClass = superClass;
  }

  public ArrayList getInterfaces() {
    return interfaces;
  }

  public void setInterfaces(ArrayList interfaces) {
    this.interfaces = interfaces;
  }
}
```


Klasse `JMethod.java`:

```java
package net.sf.regain.crawler.preparator.java;

import java.util.ArrayList;

public class JMethod {
  private String methodName = null;
  private ArrayList parameters = new ArrayList();
  private String codeBlock = null;
  private String returnType = null;

  public String getMethodName() {
    return methodName;
  }

  public void setMethodName(String methodName) {
    this.methodName = methodName;
  }

  public ArrayList getParameters() {
    return parameters;
  }

  public void setParameters(ArrayList parameters) {
    this.parameters = parameters;
  }

  public String getCodeBlock() {
    return codeBlock;
  }

  public void setCodeBlock(String codeBlock) {
    this.codeBlock = codeBlock;
  }

  public String getReturnType() {
    return returnType;
  }

  public void setReturnType(String returnType) {
    this.returnType = returnType;
  }
}
```


Siehe auch
----------

  * [howto](/de/howto/) - Übersicht über alle How-Tos
  * [Using Lucene to Search Java Source Code](http://www.onjava.com/pub/a/onjava/2006/01/18/using-lucene-to-search-java-source.html?page=1)
  * [Exploring Eclipse's ASTParser](http://www-128.ibm.com/developerworks/opensource/library/os-ast/)
