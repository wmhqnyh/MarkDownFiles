##处理Gif问题相关

目前Android处理动图的Lib主要是：**Glide，Fresco，Android-gif-drawable，gifView**等

**1.Glide**

Github项目地址：https://github.com/bumptech/glide

1.	You can download a jar from GitHub's releases page.
2.	Or use Gradle:

		repositories {
			mavenCentral() // jcenter() works as well because it pulls from Maven Central
		}
	
		dependencies {
		  compile 'com.github.bumptech.glide:glide:3.7.0'
		  compile 'com.android.support:support-v4:19.1.0'
		}

3. Or Maven:

		<dependency>
		  <groupId>com.github.bumptech.glide</groupId>
		  <artifactId>glide</artifactId>
		  <version>3.7.0</version>
		</dependency>
		<dependency>
		  <groupId>com.google.android</groupId>
		  <artifactId>support-v4</artifactId>
		  <version>r7</version>
		</dependency>


Proguard:

		-keep public class * implements com.bumptech.glide.module.GlideModule
		-keep public enum com.bumptech.glide.load.resource.bitmap.ImageHeaderParser$** {
		  **[] $VALUES;
		  public *;
		}
	
		# for DexGuard only
		-keepresourcexmlelements manifest/application/meta-data@value=GlideModule



**2.FaceBook脸书旗下的Fresco**

Github项目地址：https://github.com/facebook/fresco

文档地址：https://www.fresco-cn.org/docs/index.html （官方文分为英文，中文和韩文版本）

编辑 build.gradle 文件:

	dependencies {
	  // 其他依赖
	  compile 'com.facebook.fresco:fresco:0.12.0'
	}

下面的依赖需要根据需求添加：

	dependencies {
	  // 在 API < 14 上的机器支持 WebP 时，需要添加
	  compile 'com.facebook.fresco:animated-base-support:0.12.0'
	
	  // 支持 GIF 动图，需要添加
	  compile 'com.facebook.fresco:animated-gif:0.12.0'
	
	  // 支持 WebP （静态图+动图），需要添加
	  compile 'com.facebook.fresco:animated-webp:0.12.0'
	  compile 'com.facebook.fresco:webpsupport:0.12.0'
	
	  // 仅支持 WebP 静态图，需要添加
	  compile 'com.facebook.fresco:webpsupport:0.12.0'
	}

  使用Eclipse 作为Android IDE的坑

	下载 zip 文件.
	解压后，你会看到一个目录：frescolib，注意这个目录。
	从菜单 “文件(File)”，选择导入(Import)
	展开 Android, 选择 “Existing Android Code into Workspace”， 下一步。
	浏览，选中刚才解压的的文件中的 frescolib 目录。
	这5个项目应该被添加到工程： drawee, fbcore, fresco, imagepipeline, imagepipeline-base。请确认这5个项目一定是被选中的。点击完成。其他的项目参考之前 Gradle的额外依赖介绍。
	右键，项目，选择属性，然后选择 Android。
	点击右下角的 Add 按钮，选择 fresco，点击 OK，再点击 OK。
	现在，fresco 就导入到项目中了，你可以开始编译了。如果编译不通过，可以尝试清理资源，或者重启 Eclipse。
	如果你想在网络层使用 OkHttp，请看这里.（地址：https://www.fresco-cn.org/docs/using-other-network-layers.html#_）
	如果 support-v4 包重复了，删掉 frescolib/imagepipeline/libs 下的即可。