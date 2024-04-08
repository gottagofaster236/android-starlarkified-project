This is an example of starlarkified Android rules breaking AARs

- Checkout commit 641168 and run `bazel build //...`. Everything compiles.
- Checkout commit d1d0dc, which switches to `rules_android`, and run `bazel build //...` again. We get the following resource compilation error:
  ```ERROR: /Users/Lev.Leontev/IdeaProjects/android-project/src/main/BUILD:3:15: Packaging Android Resources in @@//src/main:app_RESOURCES_DO_NOT_USE failed: (Exit 1): java failed: error executing PackageAndroidResources command (from target //src/main:app_RESOURCES_DO_NOT_USE) external/rules_java~~toolchains~remotejdk11_macos_aarch64/bin/java -Xms4G -Xmx4G -XX:+ExitOnOutOfMemoryError -jar ... (remaining 33 arguments skipped)

  Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
  Apr 08, 2024 4:05:13 PM com.google.devtools.build.android.ResourceProcessorBusyBox processRequest
  SEVERE: Error during processing
  java.lang.RuntimeException: Error during Linking bazel-out/darwin_arm64-fastbuild/bin/src/main/_migrated/app_RESOURCES_DO_NOT_USEadd_g3itr/AndroidManifest.xml:
  Command: bazel-out/darwin_arm64-opt-exec-ST-13d3ddad9198/bin/external/rules_android~~android_sdk_repository_extension~androidsdk/aapt2_binary\
  	link\
  	--no-version-vectors\
  	--no-static-lib-packages\
  	--manifest\
  	bazel-out/darwin_arm64-fastbuild/bin/src/main/_migrated/app_RESOURCES_DO_NOT_USEadd_g3itr/AndroidManifest.xml\
  	--auto-add-overlay\
  	--proto-format\
  	--debug-mode\
  	--custom-package\
  	main\
  	-I\
  	external/rules_android~~android_sdk_repository_extension~androidsdk/platforms/android-34/android.jar\
  	-R\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/filtered/bazel-out/darwin_arm64-fastbuild-android-ST-80dd4ae33d52/bin/src/main/java/com/example/myapplication/_migrated/lib_symbols/symbols.zip\
  	-R\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/filtered/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/compiled/compiled.zip\
  	--output-text-symbols\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/R.txt\
  	--emit-ids\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/ids.txt\
  	--java\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/java\
  	--proguard\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/proguard.cfg\
  	--proguard-main-dex\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/proguard.maindex.cfg\
  	--no-proguard-location-reference\
  	-o\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/bin.-pb.apk
  Output:
  src/main/java/com/example/myapplication/res/layout/activity_main.xml:6: error: resource string/search_menu_title (aka com.example.myapplication:string/search_menu_title) not found.
  error: failed linking file resources.
  
  	at com.google.devtools.build.android.CommandHelper.execute(CommandHelper.java:42)
  	at com.google.devtools.build.android.AaptCommandBuilder.execute(AaptCommandBuilder.java:286)
  	at com.google.devtools.build.android.aapt2.ResourceLinker.linkProtoApk(ResourceLinker.java:483)
  	at com.google.devtools.build.android.aapt2.ResourceLinker.link(ResourceLinker.java:672)
  	at com.google.devtools.build.android.Aapt2ResourcePackagingAction.main(Aapt2ResourcePackagingAction.java:513)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox$Tool$8.call(ResourceProcessorBusyBox.java:112)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.processRequest(ResourceProcessorBusyBox.java:237)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.main(ResourceProcessorBusyBox.java:184)
  
  Exception in thread "main" java.lang.RuntimeException: Error during Linking bazel-out/darwin_arm64-fastbuild/bin/src/main/_migrated/app_RESOURCES_DO_NOT_USEadd_g3itr/AndroidManifest.xml:
  Command: bazel-out/darwin_arm64-opt-exec-ST-13d3ddad9198/bin/external/rules_android~~android_sdk_repository_extension~androidsdk/aapt2_binary\
  	link\
  	--no-version-vectors\
  	--no-static-lib-packages\
  	--manifest\
  	bazel-out/darwin_arm64-fastbuild/bin/src/main/_migrated/app_RESOURCES_DO_NOT_USEadd_g3itr/AndroidManifest.xml\
  	--auto-add-overlay\
  	--proto-format\
  	--debug-mode\
  	--custom-package\
  	main\
  	-I\
  	external/rules_android~~android_sdk_repository_extension~androidsdk/platforms/android-34/android.jar\
  	-R\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/filtered/bazel-out/darwin_arm64-fastbuild-android-ST-80dd4ae33d52/bin/src/main/java/com/example/myapplication/_migrated/lib_symbols/symbols.zip\
  	-R\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/filtered/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/compiled/compiled.zip\
  	--output-text-symbols\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/R.txt\
  	--emit-ids\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/ids.txt\
  	--java\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/java\
  	--proguard\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/proguard.cfg\
  	--proguard-main-dex\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/proguard.maindex.cfg\
  	--no-proguard-location-reference\
  	-o\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp11806426057367893463/linked/bin.-pb.apk
  Output:
  src/main/java/com/example/myapplication/res/layout/activity_main.xml:6: error: resource string/search_menu_title (aka com.example.myapplication:string/search_menu_title) not found.
  error: failed linking file resources.
  
  	at com.google.devtools.build.android.CommandHelper.execute(CommandHelper.java:42)
  	at com.google.devtools.build.android.AaptCommandBuilder.execute(AaptCommandBuilder.java:286)
  	at com.google.devtools.build.android.aapt2.ResourceLinker.linkProtoApk(ResourceLinker.java:483)
  	at com.google.devtools.build.android.aapt2.ResourceLinker.link(ResourceLinker.java:672)
  	at com.google.devtools.build.android.Aapt2ResourcePackagingAction.main(Aapt2ResourcePackagingAction.java:513)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox$Tool$8.call(ResourceProcessorBusyBox.java:112)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.processRequest(ResourceProcessorBusyBox.java:237)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.main(ResourceProcessorBusyBox.java:184)
  ERROR: /Users/Lev.Leontev/IdeaProjects/android-project/src/main/java/com/example/myapplication/BUILD:7:16: Linking Android Resources in src/main/java/com/example/myapplication/_migrated/lib_files/library.ap_ failed: (Exit 1): java failed: error executing LinkAndroidResources command (from target //src/main/java/com/example/myapplication:lib) external/rules_java~~toolchains~remotejdk11_macos_aarch64/bin/java -Xms4G -Xmx4G -XX:+ExitOnOutOfMemoryError -jar ... (remaining 20 arguments skipped)
  
  Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
  Apr 08, 2024 4:05:13 PM com.google.devtools.build.android.ResourceProcessorBusyBox processRequest
  SEVERE: Error during processing
  java.lang.RuntimeException: Error during Statically linking com.google.devtools.build.android.aapt2.CompiledResources@3e08ff24:
  Command: bazel-out/darwin_arm64-opt-exec-ST-13d3ddad9198/bin/external/rules_android~~android_sdk_repository_extension~androidsdk/aapt2_binary\
  	link\
  	--static-lib\
  	--manifest\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/manifest-aapt-dummy/AndroidManifest.xml\
  	--no-static-lib-packages\
  	--no-version-vectors\
  	-R\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/filtered/bazel-out/darwin_arm64-fastbuild/bin/src/main/java/com/example/myapplication/_migrated/lib_symbols/symbols.zip\
  	-I\
  	external/rules_android~~android_sdk_repository_extension~androidsdk/platforms/android-34/android.jar\
  	--auto-add-overlay\
  	-o\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/lib.apk\
  	--java\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/java\
  	--output-text-symbols\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/R.txt
  Output:
  src/main/java/com/example/myapplication/res/layout/activity_main.xml:6: error: resource string/search_menu_title (aka com.example.myapplication:string/search_menu_title) not found.
  error: failed linking file resources.
  
  	at com.google.devtools.build.android.CommandHelper.execute(CommandHelper.java:42)
  	at com.google.devtools.build.android.AaptCommandBuilder.execute(AaptCommandBuilder.java:286)
  	at com.google.devtools.build.android.aapt2.ResourceLinker.linkStatically(ResourceLinker.java:295)
  	at com.google.devtools.build.android.ValidateAndLinkResourcesAction.main(ValidateAndLinkResourcesAction.java:235)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox$Tool$7.call(ResourceProcessorBusyBox.java:106)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.processRequest(ResourceProcessorBusyBox.java:237)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.main(ResourceProcessorBusyBox.java:184)
  
  Exception in thread "main" java.lang.RuntimeException: Error during Statically linking com.google.devtools.build.android.aapt2.CompiledResources@3e08ff24:
  Command: bazel-out/darwin_arm64-opt-exec-ST-13d3ddad9198/bin/external/rules_android~~android_sdk_repository_extension~androidsdk/aapt2_binary\
  	link\
  	--static-lib\
  	--manifest\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/manifest-aapt-dummy/AndroidManifest.xml\
  	--no-static-lib-packages\
  	--no-version-vectors\
  	-R\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/filtered/bazel-out/darwin_arm64-fastbuild/bin/src/main/java/com/example/myapplication/_migrated/lib_symbols/symbols.zip\
  	-I\
  	external/rules_android~~android_sdk_repository_extension~androidsdk/platforms/android-34/android.jar\
  	--auto-add-overlay\
  	-o\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/lib.apk\
  	--java\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/java\
  	--output-text-symbols\
  	/var/folders/_m/zb9s78n177n05q15x50dqwwh0000gp/T/android_resources_tmp8303666499119102049/R.txt
  Output:
  src/main/java/com/example/myapplication/res/layout/activity_main.xml:6: error: resource string/search_menu_title (aka com.example.myapplication:string/search_menu_title) not found.
  error: failed linking file resources.
  
  	at com.google.devtools.build.android.CommandHelper.execute(CommandHelper.java:42)
  	at com.google.devtools.build.android.AaptCommandBuilder.execute(AaptCommandBuilder.java:286)
  	at com.google.devtools.build.android.aapt2.ResourceLinker.linkStatically(ResourceLinker.java:295)
  	at com.google.devtools.build.android.ValidateAndLinkResourcesAction.main(ValidateAndLinkResourcesAction.java:235)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox$Tool$7.call(ResourceProcessorBusyBox.java:106)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.processRequest(ResourceProcessorBusyBox.java:237)
  	at com.google.devtools.build.android.ResourceProcessorBusyBox.main(ResourceProcessorBusyBox.java:184)
  Use --verbose_failures to see the command lines of failed build steps.
  INFO: Elapsed time: 50.814s, Critical Path: 23.43s
  INFO: 833 processes: 70 internal, 725 darwin-sandbox, 38 worker.
  ERROR: Build did NOT complete successfully
  ```
