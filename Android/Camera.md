> Thinking

```
Manifest.permission.CAMERA
Camera
	getParameters setParameters
	setPreviewDisplay # Camera.PreviewCallback onPreviewFrame
	autoFocus # Camera.AutoFocusCallback onAutoFocus
	startPreview stopPreview # 开始停止预览
	takePicture # 照相
		# Camera.ShutterCallback onShutter
		# Camera.PictureCallback onPictureTaken (byte[] data, Camera camera)
	open
	release
	setDisplayOrientation # 90 Portrait mode
	lock unlock
	getNumberOfCameras # 摄像头数目 判断手机是否存在摄像头 context.getPackageManager().hasSystemFeature(PackageManager.FEATURE_CAMERA) ? 1 : 0;
	getCameraInfo # Camera.CameraInfo
	setOneShotPreviewCallback # Camera.PreviewCallback onPreviewFrame
Camera.CameraInfo
	CAMERA_FACING_FRONT CAMERA_FACING_BACK
	facing
	orientation
Camera.Parameters
	<flash mode>
	getSupportedPreviewSizes # 预览尺寸 预览像素 Camera.Size width height
	getSupportedPictureSizes # Camera.Size width height
	getPictureSize setPictureSize # 设置照片的大小
	getSupportedPreviewFpsRange # 预览帧率
	getSupportedPreviewFormats # 颜色格式
	getPreviewFpsRange setPreviewFpsRange
	getPreviewSize setPreviewSize # 设置预览照片的大小
	getPreviewFrameRate setPreviewFrameRate # 帧率 每秒几帧
	getPictureFormat setPictureFormat # 设置照片的输出格式 PixelFormat.JPEG
	getPreviewFormat setPreviewFormat # ImageFormat.NV21 YV12
	getFlashMode setFocusMode # 聚焦 Camera.Parameters.FOCUS_MODE_CONTINUOUS_VIDEO
	getFlashMode setFlashMode # Camera.Parameters.FLASH_MODE_AUTO
		# Camera.Parameters.FLASH_MODE_TORCH 打开
		# Camera.Parameters.FLASH_MODE_OFF 关闭
	getWhiteBalance setWhiteBalance # 白平衡 Camera.Parameters.WHITE_BALANCE_AUTO
	getSceneMode setSceneMode # 闪光灯 Camera.Parameters.SCENE_MODE_AUTO
	set # 照片质量 ("jpeg-quality", 85)
	flatten unflatten # reset
	setRotation
SurfaceView
	getHolder


CameraManager
check Manifest.permission.CAMERA
api Build.VERSION_CODES.LOLLIPOP

CameraManager # Context.CAMERA_SERVICE
	getCameraIdList
	getCameraCharacteristics # cameraId
	openCamera # CameraDevice.StateCallback onOpened onDisconnected onError

CameraCharacteristics
	get # CameraCharacteristics.LENS_FACING
		# CameraMetadata.LENS_FACING_BACK LENS_FACING_FRONT LENS_FACING_EXTERNAL

CameraDevice
	close


```

> Memory

```

```

