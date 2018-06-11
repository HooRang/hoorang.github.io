 
## APK sign bat ##

	@echo.============= Start Sign APK=============

	@rem please set params with []

	jarsigner -verbose -digestalg SHA1 -sigalg SHA1withRSA -keystore *.keystore -storepass xxxx -keypass xxxx "%~1" xxx
	pause

    
