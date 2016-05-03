project(MultiMC_logic)

include (UnitTest)

set(CORE_SOURCES
	# LOGIC - Base classes and infrastructure
	BaseInstaller.h
	BaseInstaller.cpp
	BaseVersionList.h
	BaseVersionList.cpp
	InstanceList.h
	InstanceList.cpp
	BaseVersion.h
	BaseInstance.h
	BaseInstance.cpp
	NullInstance.h
	MMCZip.h
	MMCZip.cpp
	MMCStrings.h
	MMCStrings.cpp

	# Prefix tree where node names are strings between separators
	SeparatorPrefixTree.h

	# WARNING: globals live here
	Env.h
	Env.cpp

	# JSON parsing helpers
	Json.h
	Json.cpp

	FileSystem.h
	FileSystem.cpp

	Exception.h

	# RW lock protected map
	RWStorage.h

	# A variable that has an implicit default value and keeps track of changes
	DefaultVariable.h

	# a smart pointer wrapper intended for safer use with Qt signal/slot mechanisms
	QObjectPtr.h

	# Compression support
	GZip.h
	GZip.cpp

	# Command line parameter parsing
	Commandline.h
	Commandline.cpp

	# Version number string support
	Version.h
	Version.cpp

	# A Recursive file system watcher
	RecursiveFileSystemWatcher.h
	RecursiveFileSystemWatcher.cpp
)

add_unit_test(FileSystem
	SOURCES FileSystem_test.cpp
	LIBS MultiMC_logic
	DATA testdata
	)

add_unit_test(GZip
	SOURCES GZip_test.cpp
	LIBS MultiMC_logic
	)

set(PATHMATCHER_SOURCES
	# Path matchers
	pathmatcher/FSTreeMatcher.h
	pathmatcher/IPathMatcher.h
	pathmatcher/MultiMatcher.h
	pathmatcher/RegexpMatcher.h
)

set(NET_SOURCES
	# network stuffs
	net/NetAction.h
	net/MD5EtagDownload.h
	net/MD5EtagDownload.cpp
	net/ByteArrayDownload.h
	net/ByteArrayDownload.cpp
	net/CacheDownload.h
	net/CacheDownload.cpp
	net/NetJob.h
	net/NetJob.cpp
	net/HttpMetaCache.h
	net/HttpMetaCache.cpp
	net/PasteUpload.h
	net/PasteUpload.cpp
	net/URLConstants.h
	net/URLConstants.cpp
)

# Game launch logic
set(LAUNCH_SOURCES
	launch/steps/PostLaunchCommand.cpp
	launch/steps/PostLaunchCommand.h
	launch/steps/PreLaunchCommand.cpp
	launch/steps/PreLaunchCommand.h
	launch/steps/TextPrint.cpp
	launch/steps/TextPrint.h
	launch/steps/Update.cpp
	launch/steps/Update.h
	launch/LaunchStep.cpp
	launch/LaunchStep.h
	launch/LaunchTask.cpp
	launch/LaunchTask.h
	launch/LoggedProcess.cpp
	launch/LoggedProcess.h
	launch/MessageLevel.cpp
	launch/MessageLevel.h
)

# Old update system
set(UPDATE_SOURCES
	updater/GoUpdate.h
	updater/GoUpdate.cpp
	updater/UpdateChecker.h
	updater/UpdateChecker.cpp
	updater/DownloadTask.h
	updater/DownloadTask.cpp
)

add_unit_test(UpdateChecker
	SOURCES updater/UpdateChecker_test.cpp
	LIBS MultiMC_logic
	DATA updater/testdata
	)

add_unit_test(DownloadTask
	SOURCES updater/DownloadTask_test.cpp
	LIBS MultiMC_logic
	DATA updater/testdata
	)

# Rarely used notifications
set(NOTIFICATIONS_SOURCES
	# Notifications - short warning messages
	notifications/NotificationChecker.h
	notifications/NotificationChecker.cpp
)

# Backend for the news bar... there's usually no news.
set(NEWS_SOURCES
	# News System
	news/NewsChecker.h
	news/NewsChecker.cpp
	news/NewsEntry.h
	news/NewsEntry.cpp
)

# Icon interface
set(ICONS_SOURCES
	# News System
	icons/IIconList.h
	icons/IIconList.cpp
)

# Minecraft services status checker
set(STATUS_SOURCES
	# Status system
	status/StatusChecker.h
	status/StatusChecker.cpp
)

# Support for Minecraft instances and launch
set(MINECRAFT_SOURCES
	# Minecraft support
	minecraft/auth/AuthSession.h
	minecraft/auth/AuthSession.cpp
	minecraft/auth/MojangAccountList.h
	minecraft/auth/MojangAccountList.cpp
	minecraft/auth/MojangAccount.h
	minecraft/auth/MojangAccount.cpp
	minecraft/auth/YggdrasilTask.h
	minecraft/auth/YggdrasilTask.cpp
	minecraft/auth/flows/AuthenticateTask.h
	minecraft/auth/flows/AuthenticateTask.cpp
	minecraft/auth/flows/RefreshTask.cpp
	minecraft/auth/flows/RefreshTask.cpp
	minecraft/auth/flows/ValidateTask.h
	minecraft/auth/flows/ValidateTask.cpp
	minecraft/onesix/OneSixUpdate.h
	minecraft/onesix/OneSixUpdate.cpp
	minecraft/onesix/OneSixInstance.h
	minecraft/onesix/OneSixInstance.cpp
	minecraft/onesix/OneSixProfileStrategy.cpp
	minecraft/onesix/OneSixProfileStrategy.h
	minecraft/onesix/OneSixVersionFormat.cpp
	minecraft/onesix/OneSixVersionFormat.h
	minecraft/launch/ModMinecraftJar.cpp
	minecraft/launch/ModMinecraftJar.h
	minecraft/launch/LaunchMinecraft.cpp
	minecraft/launch/LaunchMinecraft.h
	minecraft/legacy/LegacyUpdate.h
	minecraft/legacy/LegacyUpdate.cpp
	minecraft/legacy/LegacyInstance.h
	minecraft/legacy/LegacyInstance.cpp
	minecraft/legacy/LwjglVersionList.h
	minecraft/legacy/LwjglVersionList.cpp
	minecraft/GradleSpecifier.h
	minecraft/MinecraftProfile.cpp
	minecraft/MinecraftProfile.h
	minecraft/MojangVersionFormat.cpp
	minecraft/MojangVersionFormat.h
	minecraft/JarMod.h
	minecraft/MinecraftInstance.cpp
	minecraft/MinecraftInstance.h
	minecraft/MinecraftVersion.cpp
	minecraft/MinecraftVersion.h
	minecraft/MinecraftVersionList.cpp
	minecraft/MinecraftVersionList.h
	minecraft/Rule.cpp
	minecraft/Rule.h
	minecraft/OpSys.cpp
	minecraft/OpSys.h
	minecraft/ParseUtils.cpp
	minecraft/ParseUtils.h
	minecraft/ProfileUtils.cpp
	minecraft/ProfileUtils.h
	minecraft/ProfileStrategy.h
	minecraft/Library.cpp
	minecraft/Library.h
	minecraft/MojangDownloadInfo.h
	minecraft/VersionBuildError.h
	minecraft/VersionFile.cpp
	minecraft/VersionFile.h
	minecraft/ProfilePatch.h
	minecraft/VersionFilterData.h
	minecraft/VersionFilterData.cpp
	minecraft/Mod.h
	minecraft/Mod.cpp
	minecraft/ModList.h
	minecraft/ModList.cpp
	minecraft/World.h
	minecraft/World.cpp
	minecraft/WorldList.h
	minecraft/WorldList.cpp

	# FTB
	minecraft/ftb/OneSixFTBInstance.h
	minecraft/ftb/OneSixFTBInstance.cpp
	minecraft/ftb/LegacyFTBInstance.h
	minecraft/ftb/LegacyFTBInstance.cpp
	minecraft/ftb/FTBProfileStrategy.h
	minecraft/ftb/FTBProfileStrategy.cpp
	minecraft/ftb/FTBPlugin.h
	minecraft/ftb/FTBPlugin.cpp

	# Assets
	minecraft/AssetsUtils.h
	minecraft/AssetsUtils.cpp

	# Forge and all things forge related
	minecraft/forge/ForgeVersion.h
	minecraft/forge/ForgeVersion.cpp
	minecraft/forge/ForgeVersionList.h
	minecraft/forge/ForgeVersionList.cpp
	minecraft/forge/ForgeXzDownload.h
	minecraft/forge/ForgeXzDownload.cpp
	minecraft/forge/LegacyForge.h
	minecraft/forge/LegacyForge.cpp
	minecraft/forge/ForgeInstaller.h
	minecraft/forge/ForgeInstaller.cpp

	# Liteloader and related things
	minecraft/liteloader/LiteLoaderInstaller.h
	minecraft/liteloader/LiteLoaderInstaller.cpp
	minecraft/liteloader/LiteLoaderVersionList.h
	minecraft/liteloader/LiteLoaderVersionList.cpp
)

add_unit_test(GradleSpecifier
	SOURCES minecraft/GradleSpecifier_test.cpp
	LIBS MultiMC_logic
	)

add_unit_test(MojangVersionFormat
	SOURCES minecraft/MojangVersionFormat_test.cpp
	LIBS MultiMC_logic
	DATA minecraft/testdata
	)

add_unit_test(Library
	SOURCES minecraft/Library_test.cpp
	LIBS MultiMC_logic
	)

# FIXME: shares data with FileSystem test
add_unit_test(ModList
	SOURCES minecraft/ModList_test.cpp
	DATA testdata
	LIBS MultiMC_logic
	)

add_unit_test(ParseUtils
	SOURCES minecraft/ParseUtils_test.cpp
	LIBS MultiMC_logic
	)

# the screenshots feature
set(SCREENSHOTS_SOURCES
	screenshots/Screenshot.h
	screenshots/ImgurUpload.h
	screenshots/ImgurUpload.cpp
	screenshots/ImgurAlbumCreation.h
	screenshots/ImgurAlbumCreation.cpp
)

set(TASKS_SOURCES
	# Tasks
	tasks/Task.h
	tasks/Task.cpp
	tasks/ThreadTask.h
	tasks/ThreadTask.cpp
	tasks/SequentialTask.h
	tasks/SequentialTask.cpp
)

set(SETTINGS_SOURCES
	# Settings
	settings/INIFile.cpp
	settings/INIFile.h
	settings/INISettingsObject.cpp
	settings/INISettingsObject.h
	settings/OverrideSetting.cpp
	settings/OverrideSetting.h
	settings/PassthroughSetting.cpp
	settings/PassthroughSetting.h
	settings/Setting.cpp
	settings/Setting.h
	settings/SettingsObject.cpp
	settings/SettingsObject.h
)

add_unit_test(INIFile
	SOURCES settings/INIFile_test.cpp
	LIBS MultiMC_logic
	)

set(JAVA_SOURCES
	# Java related code
	java/launch/CheckJava.cpp
	java/launch/CheckJava.h
	java/JavaChecker.h
	java/JavaChecker.cpp
	java/JavaCheckerJob.h
	java/JavaCheckerJob.cpp
	java/JavaInstall.h
	java/JavaInstall.cpp
	java/JavaInstallList.h
	java/JavaInstallList.cpp
	java/JavaUtils.h
	java/JavaUtils.cpp
	java/JavaVersion.h
	java/JavaVersion.cpp
)

add_unit_test(JavaVersion
	SOURCES java/JavaVersion_test.cpp
	LIBS MultiMC_logic
	)

set(TRANSLATIONS_SOURCES
	# Translations
	trans/TranslationDownloader.h
	trans/TranslationDownloader.cpp
)

set(TOOLS_SOURCES
	# Tools
	tools/BaseExternalTool.cpp
	tools/BaseExternalTool.h
	tools/BaseProfiler.cpp
	tools/BaseProfiler.h
	tools/JProfiler.cpp
	tools/JProfiler.h
	tools/JVisualVM.cpp
	tools/JVisualVM.h
	tools/MCEditTool.cpp
	tools/MCEditTool.h
)

set(WONKO_SOURCES
	# Wonko
	wonko/tasks/BaseWonkoEntityRemoteLoadTask.cpp
	wonko/tasks/BaseWonkoEntityRemoteLoadTask.h
	wonko/tasks/BaseWonkoEntityLocalLoadTask.cpp
	wonko/tasks/BaseWonkoEntityLocalLoadTask.h
	wonko/format/WonkoFormatV1.cpp
	wonko/format/WonkoFormatV1.h
	wonko/format/WonkoFormat.cpp
	wonko/format/WonkoFormat.h
	wonko/BaseWonkoEntity.cpp
	wonko/BaseWonkoEntity.h
	wonko/WonkoVersionList.cpp
	wonko/WonkoVersionList.h
	wonko/WonkoVersion.cpp
	wonko/WonkoVersion.h
	wonko/WonkoIndex.cpp
	wonko/WonkoIndex.h
	wonko/WonkoUtil.cpp
	wonko/WonkoUtil.h
	wonko/WonkoReference.cpp
	wonko/WonkoReference.h
)

add_unit_test(WonkoIndex
	SOURCES wonko/WonkoIndex_test.cpp
	LIBS MultiMC_logic
	)

################################ COMPILE ################################

# we need zlib
find_package(ZLIB REQUIRED)

set(LOGIC_SOURCES
	${CORE_SOURCES}
	${PATHMATCHER_SOURCES}
	${NET_SOURCES}
	${LAUNCH_SOURCES}
	${UPDATE_SOURCES}
	${NOTIFICATIONS_SOURCES}
	${NEWS_SOURCES}
	${STATUS_SOURCES}
	${MINECRAFT_SOURCES}
	${SCREENSHOTS_SOURCES}
	${TASKS_SOURCES}
	${SETTINGS_SOURCES}
	${JAVA_SOURCES}
	${TRANSLATIONS_SOURCES}
	${TOOLS_SOURCES}
	${WONKO_SOURCES}
	${ICONS_SOURCES}
)

add_library(MultiMC_logic SHARED ${LOGIC_SOURCES})
set_target_properties(MultiMC_logic PROPERTIES CXX_VISIBILITY_PRESET hidden VISIBILITY_INLINES_HIDDEN 1)

generate_export_header(MultiMC_logic)

# Link
target_link_libraries(MultiMC_logic xz-embedded unpack200 ${QUAZIP_LIBRARIES} nbt++ ${ZLIB_LIBRARIES})
qt5_use_modules(MultiMC_logic Core Xml Network Concurrent)
add_dependencies(MultiMC_logic QuaZIP)

# Mark and export headers
target_include_directories(MultiMC_logic PUBLIC "${CMAKE_CURRENT_BINARY_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}" PRIVATE "${ZLIB_INCLUDE_DIRS}")