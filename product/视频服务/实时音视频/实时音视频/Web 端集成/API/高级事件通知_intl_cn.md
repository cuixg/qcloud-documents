基础事件通知包括 PeerConnection 连接通知的通知。详细描述如下：

### onStreamNotify
视频流事件通知。

#### 语法示例
```javascript
    RTC.on( 'onStreamNotify' , function( info ){ })
```

#### info

| 参数        | 类型     | 描述           |
| --------- | ------ | ------------ |
| event | String | onadd:音视频流新增   onactive:音视频流断开 |
| isLocal | Bool | 是否本地流 |
| stream | Stream | 是否本地流 |
| type | 类型 | stream/audio/video (stream作为audio和video track的载体，如果类型是stream,则表示流断开了)|

#### 代码示例
```javascript
    RTC.on( 'onStreamNotify' , function( info ){
        
    })
```



### onErrorNotify
错误时间通知

#### 语法示例
```javascript
    RTC.on( 'onErrorNotify' , function( info ){ })
```

#### info

| 参数        | 类型     | 描述           |
| --------- | ------ | ------------ |
| errorCode | Integer | 错误码 |
| errorMsg | String | 错误信息 |

#### 代码示例
```javascript
    RTC.on( 'onErrorNotify' , function( info ){
        
    })
```




### onWebSocketNotify
websocket 事件通知

#### 语法示例
```javascript
    RTC.on( 'onWebSocketNotify' , function( info ){ })
```

#### info

| 参数        | 类型     | 描述           |
| --------- | ------ | ------------ |
| errorCode | Integer | 错误码 |
| errorMsg | String | 错误信息 |
| extInfo | Object | websocket具体信息 |


#### 代码示例
```javascript
    var error_code_map = WebRTCAPI.fn.getErrorCode();
    
    RTC.on( 'onWebsocketNotify' , function( info ){
        switch( info.errorCode ){
            case 0:
                // conn succ
                break;
            case error_code_map.WS_CLOSE:
                // close
                console.warn( info );
                break;
            case error_code_map.WS_ERROR:
                // error
                console.error( info );
                break;
            default:
                break;
        }
    })
```


### onPeerConnectionAdd
PeerConnection 连接通知。通过这个通知，可以在建立p2p连接前由业务侧决定是否需要连接。需要结合实例化的参数 peerAddNotify  使用

我们的demo 代码中，也有 peerconnection 的示例可以参考

#### 语法示例
```javascript
    RTC.on( 'onPeerConnectionAdd' , function( info ){ })
```



#### info

| 参数        | 类型     | 描述           |
| --------- | ------ | ------------ |
| userId | String | 连接所属用户用户名 |
| tinyId | String | 连接所属用户用户名在腾讯云对应的唯一64位id，这里你无需理解这个参数的作用，只需在startRTC的时候透传即可。 |

#### 代码示例
```javascript
    RTC.on( 'onPeerConnectionAdd' , function( info ){
        //由业务决定，是否要建立peerconnection
        if( info.userId === '指定用户名'){
            WebRTCAPI.startRTC( info );
        }else{
            console.debug('不建立连接')
        }
    })
```