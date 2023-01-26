<!--
 * @Description: The world is better because of you
 * @Author: Lion
 * @version: 0.17.0
 * @Date: 2023-01-26 18:37:07
 * @LastEditors: VsCode Editor
 * @LastEditTime: 2023-01-26 18:52:02
-->
# Zebra Messenger API Document 

## Zebra Messenger Service Type:
    IM  Message   Service
    API Message   Service
    File Proxy    Service
    Call Service

## Server Address Type:
    pub enum AntHostType {
        TCP = 1, //raw tcp connection
        HTTP = 2,// http connection
        HTTP2 = 3,// http2 connection
        WEBSOCKET = 4, // websocket connection
        UDP = 5,// udp connection
        SOCKS5 = 6, //socks5 proxy connection
        SOCKS5H = 7,// socke5h proxy connection
    }
## Server Host Info DataStruct:

struct AntHostInfo {
    
    pub host:String, // ip or domain
    pub ssl:bool,// ssl enabled
    pub proxy:bool, // proxy 
    pub protocol:i32, // AntHostType
    pub domain:Option<String>,//optional domain 
    #[serde(rename = "cdnNumber")]
    pub cdn_id:i32,// defualt 0 
    pub port:u16,//host port

    //client sdk
    pub username:Option<String>, //proxy server username optional socks5 https or http proxy server 
    pub password:Option<String>,
    #[serde(rename = "connectTimeout")]
    pub connect_timeout:i32,//default 15s
    pub nodelay:bool, //default true
    pub gzip:bool,//default false
    pub timeout:i32,//default 30s
    #[serde(rename = "idleTimeout")]
    pub idle_timeout:i32,//defaut 90s
    #[serde(rename = "tcpKeepAlive")]
    pub tcp_keep_alive:i32,//tcp keep alive only http2
    #[serde(rename = "maxIdle")]
    pub max_idle:i32,// only http2
    #[serde(rename = "windowSize")]
    pub window_size:u32,//only http2
    #[serde(rename = "maxFrameSize")]
    pub max_frame_size:u32,//only http2
    #[serde(rename = "keepAliveInterval")]
    pub keep_alive_interval:i32,//only http2
    #[serde(rename = "keepAliveTimeOut")]
    pub keep_alive_time_out:i32,//only http2

}


## SDK Logical Architecture

======================= | ===================================
== MessageController == | == UtilsTools | Logs | Encrypts ===
========================| ===================================
== Messages Services  ==| == File Serivces | Task Services ==
========================|====================================
== Tcp / Websockets ====|=== sqlite3 database ===============
==============================================================


## SDK Components:

MessageController


### MessageController

