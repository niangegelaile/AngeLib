# AngeLib
a android lib
把lib上传到https://bintray.com；
步骤：
1.注册账号
 ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/register.png)
 2.添加配置
 ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/1.png)
 ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/2.png)
 ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/3.png)

 def siteUrl = 'https://github.com/niangegelaile/AngeLib' // 项目的主页
def gitUrl = 'https://github.com/niangegelaile/AngeLib.git' // Git仓库的url
group = "cn.com.ange" // Maven Group ID for the artifact，一般填你唯一的包名
install {
    repositories.mavenInstaller {
        // This generates POM.xml with proper parameters
        pom {
            project {
                packaging 'aar'
                // Add your description here
                name 'Android lib' //项目描述
                url siteUrl
                // Set your license
                licenses {
                    license {
                        name 'The Apache Software License, Version 2.0'
                        url 'http://www.apache.org/licenses/LICENSE-2.0.txt'
                    }
                }
                developers {
                    developer {
                        id 'cetian'    //填写的一些基本信息
                        name 'ce tian'    //你的名字
                        email '13750523051@sina.cn'//你的邮箱
                    }
                }
                scm {
                    connection gitUrl
                    developerConnection gitUrl
                    url siteUrl
                }
            }
        }
    }
}
task sourcesJar(type: Jar) {
    from android.sourceSets.main.java.srcDirs
    classifier = 'sources'
}
task javadoc(type: Javadoc) {
    source = android.sourceSets.main.java.srcDirs
    classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
}
task javadocJar(type: Jar, dependsOn: javadoc) {
    classifier = 'javadoc'
    from javadoc.destinationDir
}
artifacts {
    archives javadocJar
    archives sourcesJar
}
Properties properties = new Properties()
properties.load(project.rootProject.file('local.properties').newDataInputStream())
bintray {
    user = properties.getProperty("bintray.user")
    key = properties.getProperty("bintray.apikey")
    configurations = ['archives']
    pkg {
        repo = "maven"
        name = "AngeLib"    //发布到JCenter上的项目名字
        websiteUrl = siteUrl
        vcsUrl = gitUrl
        licenses = ["Apache-2.0"]
        publish = true
    }
}

 ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/4.png)
 注意对应字段（不要填错）：
  ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/5.png)
   ![image](https://github.com/niangegelaile/AngeLib/blob/master/images-folder/6.png)
