Requirements
------------

* [SBT 0.13+](http://www.scala-sbt.org/)

Installation
------------

Until this is published to a Maven repository, add the following lines to project/plugins.sbt (project-specific):

    lazy val root = project.in( file(".") ) dependsOn (junitXmlListener)

    lazy val junitXmlListener = uri("git://github.com/fupelaqu/junit_xml_listener.git#patch-1")

This will add the dependency to the plugin. The next step is to configure your build to output the XML. The following will output the XML in ${crossTarget}/test-reports:

    import eu.henkelmann.sbt._
    
    testListeners <<= crossTarget.map(t => Seq(new JUnitXmlTestsListener(t.getAbsolutePath)))

Note that the line as shown is enough in a *.sbt file. In *.scala files (full configuration), you must collect the result of the expression into the settings of all projects that should produce the XML output.
