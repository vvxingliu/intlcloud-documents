TRTCCalling은 Tencent Cloud TRTC와 IM 서비스를 결합한 것으로, 일대일 멀티미디어 통화를 지원합니다. TRTCCalling은 오픈 소스 Class로 Tencent Cloud의 2개의 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [실시간 영상 통화(Flutter)](https://intl.cloud.tencent.com/zh/document/product/647)를 참조하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)를 사용하는 저딜레이 멀티미디어 통화 모듈입니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047)를 사용하여 신호 메시지를 발송 및 처리합니다.


<h2 id="TRTCCalling">TRTCCalling API 개요</h2>

### SDK 기본 함수

| API                                             | 설명                                          |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | 모듈 단일 항목입니다.                                       |
| [destroySharedInstance](#destroysharedinstance) | 모듈 단일 항목을 폐기합니다.                                   |
| [registerListener](#registerlistener)           | 이벤트 콜백을 추가합니다.                                   |
| [unRegisterListener](#unregisterlistener)       | 콜백 인터페이스를 삭제합니다.                                   |
| [destroy](#destroy)                             | 함수를 폐기합니다. 해당 인스턴스를 다시 실행할 필요가 없는 경우 해당 인터페이스를 호출하십시오.   |
| [login](#login)                                 | 모듈 인터페이스에 로그인합니다. 모든 기능은 먼저 로그인한 후 사용할 수 있습니다. |
| [logout](#logout)                               | 모듈 인터페이스에서 로그아웃합니다. 로그아웃한 후에는 발신 기능을 사용할 수 없습니다.         |


### 통화 작업 관련 인터페이스 함수

| API               | 설명           |
| ----------------- | -------------- |
| [call](#call)     | 1명을 통화에 초대합니다. |
| [accept](#accept) | 현재 통화를 수신합니다. |
| [reject](#reject) | 현재 통화를 거절합니다. |
| [hangup](#hangup) | 현재 통화를 종료합니다. |

### 푸시/풀 스트림 관련 인터페이스 함수

| API                                 | 설명                                                   |
| ----------------------------------- | ------------------------------------------------------ |
| [startRemoteView](#startremoteview) | 원격 사용자의 카메라 데이터를 지정한 TXCloudVideoView로 렌더링합니다.  |
| [stopRemoteView](#stopremoteview)   | 원격 데이터 렌더링을 종료합니다.                                     |

### 멀티미디어 제어 관련 인터페이스 함수

| API                           | 설명                                             |
| ----------------------------- | ------------------------------------------------ |
| [openCamera](#opencamera)     | 카메라를 활성화해 지정한 TXCloudVideoView로 렌더링합니다. |
| [switchCamera](#switchcamera) | 전후면 카메라를 전환합니다.                                 |
| [closeCamara](#closecamara)   | 카메라를 비활성화합니다.                                     |
| [setMicMute](#setmicmute)     | 로컬 오디오 샘플링을 음소거합니다.                               |
| [setHandsFree](#sethandsfree) | 핸즈프리를 설정합니다.                             |

<h2 id="TRTCCallingDelegate">TRTCCallingDelegate API 개요</h2>

### 일반적인 이벤트 콜백

| API                 | 설명       |
| ------------------- | ---------- |
| [onError](#onerror) | 오류 콜백입니다. |

### 초대 발신자 콜백

| API                       | 설명             |
| ------------------------- | ---------------- |
| [onReject](#onreject)     | 통화 거절 콜백입니다.   |
| [onNoResp](#onnoresp)     | 상대방 응답 없음 콜백입니다. |
| [onLineBusy](#onlinebusy) | 통화 중 콜백입니다.   |

### 초대 수신자 콜백

| API                                   | 설명                 |
| ------------------------------------- | -------------------- |
| [onInvited](#oninvited)               | 통화에 초대됨 콜백입니다.     |
| [onCallingCancel](#oncallingcancel)   | 현재 통화 취소됨 콜백입니다. |
| [onCallingTimeOut](#oncallingtimeout) | 현재 통화 시간 초과 콜백입니다.   |

### 범용 콜백

| API  | 설명 |
| ---- | ---- |
| [onUserEnter](#onuserenter)                                  | 사용자 통화 입장 콜백입니다.         |
| [onUserLeave](#onuserleave)                                  | 사용자 통화 종료 콜백입니다.         |
| [onUserAudioAvailable](#onuseraudioavailable)                | 사용자의 오디오 업스트림 활성화 여부 콜백입니다. |
| [onUserVideoAvailable](#onuservideoavailable)                | 사용자의 비디오 업스트림 활성화 여부 콜백입니다. |
| [onUserVoiceVolume](#onuservoicevolume)                      | 사용자 통화 음량 콜백입니다.         |
| [onCallEnd](#oncallend)                                      | 통화 종료 콜백입니다.             |

## SDK 기본 함수

### sharedInstance

sharedInstance는 TRTCCalling의 모듈 단일 항목입니다.

```java
static Future<TRTCCalling> sharedInstance();
```

### destroySharedInstance

모듈 단일 항목을 폐기합니다.

```java
static void destroySharedInstance();
```

### destroy

함수를 폐기합니다. 해당 인스턴스를 다시 실행할 필요가 없는 경우 해당 인터페이스를 호출하십시오.

```java
void destroy();
```

### registerListener

[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066) 이벤트 콜백입니다. TRTCCallingDelegate에서 [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066)의 각종 상태 공지를 확인할 수 있습니다.

```java
void registerListener(VoiceListenerFunc func);
```

### unRegisterListener

콜백 인터페이스를 삭제합니다.

```java
void unRegisterListener(VoiceListenerFunc func);
```

### login

모듈에 로그인합니다.

```java
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 의미                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| sdkAppID | UInt32 | TRTC 콘솔 > [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) > 애플리케이션 정보에서 SDKAppID를 조회할 수 있습니다. |
| userId   | String | 현재 사용자의 ID입니다. 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig  | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |

### logout

모듈에서 로그아웃하였습니다.

```java
Future<ActionCallback> logout();
```

## 통화 작업 관련 인터페이스 함수

### call

1인 통화 초대는 현재 통화 중이더라도 계속 다른 사람을 초대할 수 있습니다.

```java
Future<ActionCallback> call(String userId, int type);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                             |
| ------ | ------ | -------------------------------- |
| userId | String | 호출 사용자 ID입니다.                    |
| type   | int    | 1은 음성 통화, 2는 영상 통화를 의미합니다. |

### accept

현재 통화를 수락합니다. 초대된 사용자가 `onInvited()` 콜백을 받으면 해당 함수를 호출해 통화를 수신할 수 있습니다.

```java
Future<ActionCallback> accept();
```

### reject

현재 통화를 거절합니다. 초대된 사용자가 `onInvited()` 콜백을 받으면 해당 함수를 호출하여 통화를 거절할 수 있습니다.

```java
Future<ActionCallback> reject();
```

### hangup

통화를 종료합니다. 통화 중이었다면 해당 함수를 호출하여 통화를 종료할 수 있습니다.

```java
void hangup();
```


## 푸시/풀 스트림 관련 인터페이스 함수

### startRemoteView

원격 사용자의 카메라 데이터를 지정한 TRTCCloudVideoView로 렌더링합니다.

```java
void startRemoteView(String userId, int streamType, int viewId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                                               |
| ------ | ------ | -------------------------------------------------- |
| userId | String | 원격 사용자 ID입니다.                                      |
| view   | int    | 비디오 화면 컨트롤러 TRTCCloudVideoView 콜백 viewId입니다. |


### stopRemoteView

원격 데이터 렌더링을 종료합니다.

```java
void stopRemoteView(String userId, int streamType);
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미                                   |
| ---------- | ------ | -------------------------------------- |
| userId     | String | 원격 사용자 ID입니다.                          |
| streamType | int    | 시청을 중지할 userId의 비디오 스트림 유형을 지정합니다. |

## 멀티미디어 제어 관련 인터페이스 함수

### openCamera

카메라를 활성화하여 지정한 TRTCCloudVideoView로 렌더링합니다.

```java
void openCamera(bool isFrontCamera, int viewId);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형 | 의미                                                |
| ------------- | ---- | --------------------------------------------------- |
| isFrontCamera | bool | true는 전면 카메라 활성화, false는 후면 카메라 활성화를 의미합니다. |
| viewId        | int  | 비디오 화면 컨트롤러 TRTCCloudVideoView를 콜백하는 viewId입니다.  |

### switchCamera

전후면 카메라를 전환합니다.

```java
void switchCamera(bool isFrontCamera);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형 | 의미                                                    |
| ------------- | ---- | ------------------------------------------------------- |
| isFrontCamera | bool | true는 전면 카메라로 전환, false는 후면 카메라로 전환을 의미합니다. |

### closeCamara

카메라를 비활성화합니다.

```java
void closeCamera();
```

### setMicMute

로컬 오디오 샘플링을 음소거합니다.

```java
void setMicMute(bool isMute);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                        |
| ------ | ---- | ------------------------------------------- |
| isMute | bool | true는 마이크 비활성화, false는 마이크 활성화를 의미합니다. |

### setHandsFree

원격 오디오를 음소거합니다.

```java
void setHandsFree(bool isHandsFree);
```

매개변수는 다음과 같습니다.

| 매개변수        | 유형 | 의미                                    |
| ----------- | ---- | --------------------------------------- |
| isHandsFree | bool | true는 핸즈프리 활성화, false는 핸즈프리 비활성화를 의미합니다. |

## TRTCCallingDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백입니다.

>?SDK가 복구할 수 없는 오류는 반드시 모니터링하고 상황에 따라 적절한 인터페이스를 사용자에게 안내해야 합니다.

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
| ---- | ------ | ---------- |
| code | int    | 에러 코드입니다.   |
| msg  | String | 오류 정보입니다. |


## 초대 발신자 콜백

### onReject

통화 거절 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미            |
| ------ | ------ | --------------- |
| userId | String | 거절한 사용자 ID입니다. |

### onNoResp

상대방이 콜백에 응답이 없습니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | ----------------- |
| userId | String | 응답이 없는 사용자 ID입니다. |

### onLineBusy

통화 중 콜백입니다.


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미            |
| ------ | ------ | --------------- |
| userId    | String  | 통화 중인 사용자 ID입니다.      |

## 초대 수신자 콜백

### onInvited

초대된 사용자 통화 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수        | 유형               | 의미                             |
| ----------- | ------------------ | -------------------------------- |
| sponsor     | String             | 발신자 ID입니다.                    |
| userIds     | List&lt;String&gt; | 본인 이외의 초대된 사용자 ID 리스트입니다.         |
| isFromGroup | bool               | 다중 사용자 통화 초대 여부               |
| type        | int                | 1은 음성 통화, 2는 영상 통화를 의미합니다. |

### onCallingCancel

현재 통화의 콜백이 취소되었습니다. 수신자가 요청을 처리하지 않은 상태에서 발신측에서 취소하면 이 콜백을 받게 됩니다.


### onCallingTimeOut

현재 통화 시간 초과 콜백입니다.


## 범용 콜백

### onUserEnter

사용자 통화 입장 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | ----------------- |
| userId | String | 통화 입장 사용자 ID입니다. |

### onUserLeave

사용자 통화 종료 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | ----------------- |
| userId    | String  | 통화 퇴장 사용자 ID입니다.      |

### onUserAudioAvailable

사용자 오디오 업스트림 활성화 여부 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| userId    | String  | 통화 사용자 ID입니다.      |
| available | boolean | 사용자의 오디오 사용 가능 여부입니다. |

### onUserVideoAvailable

사용자 비디오 업스트림 활성화 여부 콜백입니다. 공지를 받은 후, 사용자는 startRemoteView 렌더링 원격 비디오를 호출할 수 있습니다.

매개변수는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| userId    | String  | 통화 사용자 ID입니다.      |
| available | boolean | 사용자의 비디오 사용 가능 여부입니다. |


### onUserVoiceVolume

사용자 통화 음량 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수        | 유형 | 의미                                            |
| ----------- | ---- | ----------------------------------------------- |
| userVolumes | List | 현재 대화 중인 모든 방 참석자 음량 범위: 0~100 |
| totalVolume | int  | 모든 원격 참석자의 총 음량 범위: 0~100         |

### onCallEnd

통화 종료 콜백입니다.
