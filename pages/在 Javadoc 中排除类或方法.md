tags:: [[tagJavadoc]], [[tagJava]]

- ## 前言
	- 可以使用 Maven 插件 [`org.apache.maven.plugins:maven-javadoc-plugin`](https://maven.apache.org/plugins/maven-javadoc-plugin/index.html) 生成项目 Javadoc
	- 为了使文档更加简洁，降低阅读难度，我们可以将一些不重要内容在文档中进行排除
- ## 方法
	- 排除`包`
		- 在插件配置中设置 `<excludePackageNames>` 标签，并将需要排除的包路径写在标签内
			- [Apache Maven Javadoc Plugin – Excluding Packages](https://maven.apache.org/plugins/maven-javadoc-plugin/examples/exclude-package-names.html)
			- [Apache Maven Javadoc Plugin – javadoc:javadoc](https://maven.apache.org/plugins/maven-javadoc-plugin/javadoc-mojo.html#excludePackageNames)
	- `@Deprecated` 排除`类`或`方法`
		- 如果需要发布已废弃的类或方法，可以使用 `<nodeprecated>true|false</nodeprecated>` 标记
			- [Apache Maven Javadoc Plugin – javadoc:javadoc](https://maven.apache.org/plugins/maven-javadoc-plugin/javadoc-mojo.html#nodeprecated)
	- `@hidden` 排除`类`或`方法`
		- JDK >= 1.9
		- 在类或方法的 Javadoc 中使用
		- 如果当前项目 JDK < 1.9，可以使用项目外部高版本 JDK 进行 Javadoc 的生成
			- [Apache Maven Javadoc Plugin – Using Alternate Javadoc Tool](https://maven.apache.org/plugins/maven-javadoc-plugin/examples/alternate-javadoc-tool.html)
- ## 示例
	- ```xml
	  <project>
	    ...
	    <build>
	      <plugins>
	        <plugin>
	          <groupId>org.apache.maven.plugins</groupId>
	          <artifactId>maven-javadoc-plugin</artifactId>
	          <version>3.7.0</version>
	          <configuration>
	            <encoding>UTF-8</encoding>
	  		  <charset>UTF-8</charset>
	  		  <docencoding>UTF-8</docencoding>
	  		  <!-- 使用外部 javadoc 命令，使高版本 jdk 才支持的 @hidden 文档注释生效
	  		       在系统里设置高版本 JDK 环境变量，例如 ${JAVA21_HOME}
	                 添加完环境变量后，需要重启 IDEA 才生效 -->
	  		  <javadocExecutable>${env.JAVA21_HOME}/bin/javadoc</javadocExecutable>
	  		  <!-- 排除不需要生成文档的包 -->
	  		  <excludePackageNames>
	  			*.internal:org.acme.exclude1.*:org.acme.exclude2
	  		  </excludePackageNames>
	  		  <!-- 文档中不生成 @Deprecated 标注废弃的类 -->
	  		  <nodeprecated>true</nodeprecated>
	            ...
	          </configuration>
	        </plugin>
	      </plugins>
	      ...
	    </build>
	    ...
	  </project>
	  ```