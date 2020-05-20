# ModuleDemo
# 模块化demo
# 1：新建一个项目,NoActivity
# 2: New Module 作为Library 添加（comlib,modulemain,modulea,moduleb）
# 3:在项目gradle.properties文件中设置一个变量 isModule  (true or false) 集成开发和组件开发切换设置
# 4：在 （modulemain,modulea,moduleb）build.gradle 中修改：
#       if（isModule.toBoole）{
#         apply plugin: 'com.android.application'
#        }else{
#         apply plugin: 'com.android.library'
#       }
#      
#       dependencies {
#            implementation fileTree(dir: 'libs', include: ['*.jar'])

#            implementation project(path:':comlib')
#            annotationProcessor 'com.alibaba:arouter-compiler:1.1.4'
#        }
#        sourceSets {
#            main {
#              if (isModule.toBoolean()) {
#                manifest.srcFile 'src/main/module/AndroidManifest.xml'
#             } else {
#                manifest.srcFile 'src/main/AndroidManifest.xml'
#                //集成开发模式下排除debug文件夹中的所有Java文件
#                java {
#                    exclude 'debug/**'
#                 }
#              }
#            }
#       }
# 注意：清单文件等资源需要根据isModule 创建不同的注册文件 集成开发时只需要注册activity，组件开发需要设置好为启动activity 

#       comlib->build.gradle中添加依赖：注意要用api 
#       api 'com.alibaba:arouter-api:1.3.1'

#     app->build.gradle中修改
#     dependencies {
#          implementation fileTree(dir: 'libs', include: ['*.jar'])

#          implementation project(path:':comlib')
#          if (!isModule.toBoolean()){
#              implementation project(path:':modulemain')
#              implementation project(path:':modulea')
#              implementation project(path:':moduleb')
#          }
#       }

# 5: ARouter 依赖包引入，跳转 参考：https://github.com/alibaba/ARouter
#
#
