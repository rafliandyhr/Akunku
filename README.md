port: 7890
socks-port: 7891
redir-port: 7892
tproxy-port: 7893
mixed-port: 7890
allow-lan: false
mode: rule
log-level: info
ipv6: false
external-controller: 127.0.0.1:9090
external-ui: folder
interface-name: masterwifinetworksolution
dns:
  enable: true
  listen: 0.0.0.0:53
  default-nameserver:
    - 8.8.8.8
    - 8.8.4.4
    - 1.1.1.1
    - 1.0.0.1
  nameserver:
    - 114.114.114.114
    - 119.29.29.29
    - 1.1.1.1
    - 1.0.0.1 
    - https://cloudflare-dns.com/dns-query
    - https://dns.google/dns-query
    - https://1.1.1.1/dns-query
    - tls://8.8.8.8:853
    - tls://dns.rubyfish.cn:853 
    - https://1.1.1.1/dns-query 
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
proxy-groups:
- name: FINAL
  type: select
  proxies:
  - Semua_PingMantul
  - MasterTrojan
  - MasterVmess
  - VidioVmess
  - MasterShadowsocks
  - MasterSnell
  - PingMantul_Trojan
  - PingMantul_Vmess
  - PingMantul_Shadowsocks
  - PingMantul_Snell
  - Gabung_Trojan
  - Gabung_Vmess
  - Vidio_Vmess
  - Gabung_Shadowsocks
  - Gabung_Snell
  - SOSMED
  - STREAMING
  - GAME
  - BOKEP
  - VIDIO
  - ZEROTIER
  - DIRECT
 
- name: Semua_PingMantul
  type: url-test
  tolerance: 100
  use:
  - TrojanMaster
  - VmessMaster
  - ShadowsocksMaster

- name: MasterTrojan
  type: select
  use:
  - TrojanMaster

- name: MasterVmess
  type: select
  use:
  - VmessMaster
  
- name: VidioVmess
  type: select
  use:
  - VmessVidio

- name: MasterShadowsocks
  type: select
  use:
  - ShadowsocksMaster
  
- name: MasterSnell
  type: select
  use:
  - SnellMaster
 
- name: PingMantul_Trojan
  type: url-test
  tolerance: 100
  use:
  - TrojanMaster

- name: PingMantul_Vmess
  type: url-test
  tolerance: 100
  use:
  - VmessMaster
 
- name: PingMantul_Shadowsocks
  type: url-test
  tolerance: 100
  use:
  - ShadowsocksMaster
  
- name: PingMantul_Snell
  type: url-test
  tolerance: 100
  use:
  - SnellMaster

- name: Gabung_Trojan
  type: load-balance
  strategy: consistent-hashing
  disable-udp: false
  use:
  - TrojanMaster

- name: Gabung_Vmess
  type: load-balance
  strategy: consistent-hashing
  disable-udp: false
  use:
  - VmessMaster
  
- name: Vidio_Vmess
  type: fallback
  strategy: consistent-hashing
  disable-udp: false
  use:
  - VmessVidio

- name: Gabung_Shadowsocks
  type: load-balance
  strategy: consistent-hashing
  disable-udp: false
  use:
  - ShadowsocksMaster
  
- name: Gabung_Snell
  type: load-balance
  strategy: consistent-hashing
  disable-udp: false
  use:
  - SnellMaster
  
- name: SOSMED
  type: fallback
  use:
  - ShadowsocksMaster
  
- name: STREAMING
  type: fallback
  use:
  - ShadowsocksMaster
  
- name: VIDIO
  type: fallback
  use:
  - ShadowsocksMaster
  
- name: GAME
  type: load-balance
  use:
  - Game
  
- name: BOKEP
  type: fallback
  use:
  - ShadowsocksMaster
  
- name: ZEROTIER
  type: load-balance
  use:
  - ShadowsocksMaster
  - VmessMaster
  - TrojanMaster
  
  
proxies-direct:
- name: "SOSMED"
  type: select
  proxies:
    -  Gabung_Trojan
  url: 'http://www.gstatic.com/generate_204'
  interval: 300
  
- name: "STREAMING"
  type: select
  proxies:
    -  Gabung_Vmess
  url: 'http://www.gstatic.com/generate_204'
  interval: 300
  
- name: "VIDIO"
  type: select
  proxies:
    -  Vidio_Vmess
  url: 'http://www.gstatic.com/generate_204'
  interval: 300
  
- name: "GAME"
  type: select
  proxies:
    -  Game
  url: 'http://www.gstatic.com/generate_204'
  interval: 300
  
- name: "BOKEP"
  type: select
  proxies:
    -  Gabung_Vmess
  url: 'http://www.gstatic.com/generate_204'
  interval: 300
  
- name: "ZEROTIER"
  type: select
  proxies:
    -  Semua_PingMantul
  url: 'http://www.gstatic.com/generate_204'
  interval: 300

proxy-providers:
  TrojanMaster:
    type: file
    path: ./TrojanMaster.yaml
    health-check:
      enable: true
      interval: 300
      lazy: true
      url: 'http://www.gstatic.com/generate_204'
      
  VmessMaster:
    type: file
    path: ./VmessMaster.yaml
    health-check:
      enable: true
      interval: 300
      lazy: true
      url: 'http://www.gstatic.com/generate_204'
      
  VmessVidio:
    type: file
    path: ./VmessVidio.yaml
    health-check:
      enable: true
      interval: 300
      lazy: true
      url: 'http://www.gstatic.com/generate_204'
      
  Game:
    type: file
    path: ./Game.yaml
    health-check:
      enable: true
      interval: 300
      lazy: true
      url: 'http://www.gstatic.com/generate_204'

  ShadowsocksMaster:
    type: file
    path: ./ShadowsocksMaster.yaml
    health-check:
      enable: true
      interval: 300
      lazy: true
      url: 'http://www.gstatic.com/generate_204'
      
  SnellMaster:
    type: file
    path: ./SnellMaster.yaml
    health-check:
      enable: true
      interval: 300
      lazy: true
      url: 'http://www.gstatic.com/generate_204'
      
rule-providers:
  LAN:
    behavior: ipcidr
    type: file
    path: ./LAN.yaml
    
  Sosmed:
    behavior: classical
    type: file
    path: ./sosmed.yaml
    
  Streaming:
    behavior: classical
    type: file
    path: ./streaming.yaml
    
  Vidio:
    behavior: classical
    type: file
    path: ./vidio.yaml
    
  Game:
    behavior: classical
    type: file
    path: ./gaming.yaml
    
  Bokep:
    behavior: classical
    type: file
    path: ./bokep.yaml
    
  Zerotier:
    behavior: classical
    type: file
    path: ./zerotier.yaml

rules:

  - IP-CIDR,192.168.0.0/16,DIRECT,no-resolve
  - IP-CIDR,10.0.0.0/8,DIRECT,no-resolve
  - IP-CIDR,172.16.0.0/12,DIRECT,no-resolve
  - IP-CIDR,127.0.0.0/8,DIRECT,no-resolve
  - IP-CIDR,100.64.0.0/10,DIRECT,no-resolve
  - IP-CIDR6,::1/128,DIRECT,no-resolve
  - IP-CIDR6,fc00::/7,DIRECT,no-resolve
  - IP-CIDR6,fe80::/10,DIRECT,no-resolve
  - IP-CIDR6,fd00::/8,DIRECT,no-resolve
  
    # Instagram-Whatsapp
  - DOMAIN-SUFFIX,cdninstagram.com,SOSMED
  - DOMAIN-SUFFIX,instagram.com,SOSMED
  - DOMAIN-SUFFIX,cdninstagram.com,SOSMED
  - DOMAIN-SUFFIX,instagram.com,SOSMED
  - DOMAIN-SUFFIX,m.me,SOSMED
  - DOMAIN-SUFFIX,oculus.com,SOSMED
  - DOMAIN-SUFFIX,oculuscdn.com,SOSMED
  - DOMAIN-SUFFIX,rocksdb.org,SOSMED
  - DOMAIN-SUFFIX,whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,whatsapp.net,SOSMED
  - DOMAIN-SUFFIX,m.me,SOSMED
  - DOMAIN-SUFFIX,oculus.com,SOSMED
  - DOMAIN-SUFFIX,oculuscdn.com,SOSMED
  - DOMAIN-SUFFIX,rocksdb.org,SOSMED
  - DOMAIN-SUFFIX,whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,whatsapp.net,SOSMED
  - DST-PORT,3478,SOSMED
  - DST-PORT,4244,SOSMED
  - DST-PORT,5222,SOSMED
  - DST-PORT,5223,SOSMED
  - DST-PORT,5228,SOSMED
  - DST-PORT,5288,SOSMED
  - DST-PORT,5242,SOSMED
  - DST-PORT,5349,SOSMED
  - DST-PORT,34784,SOSMED
  - DST-PORT,45395,SOSMED
  - DST-PORT,50318,SOSMED
  - DST-PORT,59234,SOSMED
  # Facebook
  - DOMAIN-SUFFIX,messenger.com,SOSMED
  - DOMAIN-SUFFIX,facebook.com,SOSMED
  - DOMAIN-SUFFIX,facebook.net,SOSMED
  - DOMAIN-SUFFIX,fb.com,SOSMED
  - DOMAIN-SUFFIX,fb.me,SOSMED
  - DOMAIN-SUFFIX,fbaddins.com,SOSMED
  - DOMAIN-SUFFIX,fbcdn.net,SOSMED
  - DOMAIN-SUFFIX,fbsbx.com,SOSMED
  - DOMAIN-SUFFIX,fbworkmail.com,SOSMED
  - DOMAIN-KEYWORD,.facebook.,SOSMED
  - DOMAIN-SUFFIX,facebookmail.com,SOSMED
  - IP-CIDR,103.4.96.0/22,SOSMED
  - IP-CIDR,129.134.0.0/17,SOSMED
  - IP-CIDR,157.240.0.0/17,SOSMED
  - IP-CIDR,173.252.64.0/19,SOSMED
  - IP-CIDR,173.252.96.0/19,SOSMED
  - IP-CIDR,179.60.192.0/22,SOSMED
  - IP-CIDR,185.60.216.0/22,SOSMED
  - IP-CIDR,204.15.20.0/22,SOSMED
  - IP-CIDR,31.13.24.0/21,SOSMED
  - IP-CIDR,31.13.64.0/18,SOSMED
  - IP-CIDR,45.64.40.0/22,SOSMED
  - IP-CIDR,66.220.144.0/20,SOSMED
  - IP-CIDR,69.171.224.0/19,SOSMED
  - IP-CIDR,69.63.176.0/20,SOSMED
  - IP-CIDR,74.119.76.0/22,SOSMED
  # Line
  - DOMAIN-SUFFIX,lin.ee,SOSMED
  - DOMAIN-SUFFIX,line.me,SOSMED
  - DOMAIN-SUFFIX,line.naver.jp,SOSMED
  - DOMAIN-SUFFIX,line-apps.com,SOSMED
  - DOMAIN-SUFFIX,line-cdn.net,SOSMED
  - DOMAIN-SUFFIX,line-scdn.net,SOSMED
  - DOMAIN-SUFFIX,nhncorp.jp,SOSMED
  - DOMAIN-SUFFIX,line.me,SOSMED
  - DOMAIN-SUFFIX,line-apps.com,SOSMED
  - DOMAIN-SUFFIX,line-scdn.net,SOSMED
  - DOMAIN-SUFFIX,naver.jp,SOSMED
  - IP-CIDR,103.2.28.0/22,SOSMED
  - IP-CIDR,119.235.224.0/21,SOSMED
  - IP-CIDR,119.235.232.0/23,SOSMED
  - IP-CIDR,119.235.235.0/24,SOSMED
  - IP-CIDR,119.235.236.0/23,SOSMED
  - IP-CIDR,125.6.146.0/24,SOSMED
  - IP-CIDR,125.6.149.0/24,SOSMED
  - IP-CIDR,125.6.190.0/24,SOSMED
  - IP-CIDR,125.209.208.0/20,SOSMED
  - IP-CIDR,203.104.103.0/24,SOSMED
  - IP-CIDR,203.104.128.0/20,SOSMED
  - IP-CIDR,203.174.66.64/26,SOSMED
  - IP-CIDR,203.174.77.0/24,SOSMED
  - IP-CIDR,103.2.30.0/23,SOSMED
  - IP-CIDR,125.209.208.0/20,SOSMED
  - IP-CIDR,147.92.128.0/17,SOSMED
  - IP-CIDR,203.104.144.0/21,SOSMED
  # Telegram
  - DOMAIN-SUFFIX,telegra.ph,SOSMED
  - DOMAIN-SUFFIX,telegram.org,SOSMED
  - DOMAIN-SUFFIX,t.me,SOSMED
  - DOMAIN-SUFFIX,tdesktop.com,SOSMED
  - DOMAIN-SUFFIX,telegram.me,SOSMED
  - DOMAIN-SUFFIX,telesco.pe,SOSMED
  # Twitter
  - DOMAIN-SUFFIX,pscp.tv,SOSMED
  - DOMAIN-SUFFIX,periscope.tv,SOSMED
  - DOMAIN-SUFFIX,t.co,SOSMED
  - DOMAIN-SUFFIX,twimg.co,SOSMED
  - DOMAIN-SUFFIX,twimg.com,SOSMED
  - DOMAIN-SUFFIX,twitpic.com,SOSMED
  - DOMAIN-SUFFIX,twitter.com,SOSMED
  - DOMAIN-SUFFIX,vine.co,SOSMED
  # Instagram-Whatsapp
  - DOMAIN-SUFFIX,cdninstagram.com,SOSMED
  - DOMAIN-SUFFIX,instagram.com,SOSMED
  - DOMAIN-SUFFIX,m.me,SOSMED
  - DOMAIN-SUFFIX,oculus.com,SOSMED
  - DOMAIN-SUFFIX,oculuscdn.com,SOSMED
  - DOMAIN-SUFFIX,rocksdb.org,SOSMED
  - DOMAIN-SUFFIX,whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,whatsapp.net,SOSMED
  # Facebook
  - DOMAIN-SUFFIX,messenger.com,SOSMED
  - DOMAIN-SUFFIX,facebook.com,SOSMED
  - DOMAIN-SUFFIX,facebook.net,SOSMED
  - DOMAIN-SUFFIX,fb.com,SOSMED
  - DOMAIN-SUFFIX,fb.me,SOSMED
  - DOMAIN-SUFFIX,fbaddins.com,SOSMED
  - DOMAIN-SUFFIX,fbcdn.net,SOSMED
  - DOMAIN-SUFFIX,fbsbx.com,SOSMED
  - DOMAIN-SUFFIX,fbworkmail.com,SOSMED
  - DOMAIN-KEYWORD,.facebook.,SOSMED
  - DOMAIN-SUFFIX,facebookmail.com,SOSMED
  # Line
  - DOMAIN-SUFFIX,lin.ee,SOSMED
  - DOMAIN-SUFFIX,line.me,SOSMED
  - DOMAIN-SUFFIX,line.naver.jp,SOSMED
  - DOMAIN-SUFFIX,line-apps.com,SOSMED
  - DOMAIN-SUFFIX,line-cdn.net,SOSMED
  - DOMAIN-SUFFIX,line-scdn.net,SOSMED
  - DOMAIN-SUFFIX,nhncorp.jp,SOSMED
  - DOMAIN-SUFFIX,line.me,SOSMED
  - DOMAIN-SUFFIX,line-apps.com,SOSMED
  - DOMAIN-SUFFIX,line-scdn.net,SOSMED
  - DOMAIN-SUFFIX,naver.jp,SOSMED
  # Telegram
  - DOMAIN-SUFFIX,telegra.ph,SOSMED
  - DOMAIN-SUFFIX,telegram.org,SOSMED
  - DOMAIN-SUFFIX,t.me,SOSMED
  - DOMAIN-SUFFIX,tdesktop.com,SOSMED
  - DOMAIN-SUFFIX,telegram.me,SOSMED
  - DOMAIN-SUFFIX,telesco.pe,SOSMED
  # Twitter
  - DOMAIN-SUFFIX,pscp.tv,SOSMED
  - DOMAIN-SUFFIX,periscope.tv,SOSMED
  - DOMAIN-SUFFIX,t.co,SOSMED
  - DOMAIN-SUFFIX,twimg.co,SOSMED
  - DOMAIN-SUFFIX,twimg.com,SOSMED
  - DOMAIN-SUFFIX,twitpic.com,SOSMED
  - DOMAIN-SUFFIX,twitter.com,SOSMED
  - DOMAIN-SUFFIX,vine.co,SOSMED
  # whatsapp
  - DOMAIN-SUFFIX,web.whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,www.whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,api.whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,v.whatsapp.net,SOSMED
  - DOMAIN-SUFFIX,whatsapp.com,SOSMED
  - DOMAIN-SUFFIX,whatsapp.net,SOSMED
  - DOMAIN-SUFFIX,wa.me,SOSMED
  # youtube
  - DOMAIN-SUFFIX,youtube.com,STREAMING
  - DOMAIN-SUFFIX,googlevideo.com,STREAMING
  - DOMAIN-SUFFIX,gvt2.com,STREAMING
  - DOMAIN-SUFFIX,ytimg.com,STREAMING
  - DOMAIN-KEYWORD,youtube,STREAMING
  - DOMAIN-SUFFIX,yt3.ggpht.com,STREAMING
  - DOMAIN-SUFFIX,youtube.is,STREAMING
  - DOMAIN-SUFFIX,youtube.it,STREAMING
  - DOMAIN-SUFFIX,youtube.jo,STREAMING
  - DOMAIN-SUFFIX,youtube.jp,STREAMING
  - DOMAIN-SUFFIX,youtube.kr,STREAMING
  - DOMAIN-SUFFIX,youtube.kz,STREAMING
  - DOMAIN-SUFFIX,youtube.la,STREAMING
  - DOMAIN-SUFFIX,youtube.lk,STREAMING
  - DOMAIN-SUFFIX,youtube.lt,STREAMING
  - DOMAIN-SUFFIX,youtube.lu,STREAMING
  - DOMAIN-SUFFIX,youtube.lv,STREAMING
  - DOMAIN-SUFFIX,youtube.ly,STREAMING
  - DOMAIN-SUFFIX,youtube.ma,STREAMING
  - DOMAIN-SUFFIX,youtube.md,STREAMING
  - DOMAIN-SUFFIX,youtube.me,STREAMING
  - DOMAIN-SUFFIX,youtube.mk,STREAMING
  - DOMAIN-SUFFIX,youtube.mn,STREAMING
  - DOMAIN-SUFFIX,youtube.mx,STREAMING
  - DOMAIN-SUFFIX,youtube.my,STREAMING
  - DOMAIN-SUFFIX,youtube.ng,STREAMING
  - DOMAIN-SUFFIX,youtube.ni,STREAMING
  - DOMAIN-SUFFIX,youtube.nl,STREAMING
  - DOMAIN-SUFFIX,youtube.no,STREAMING
  - DOMAIN-SUFFIX,youtube.pa,STREAMING
  - DOMAIN-SUFFIX,youtube.pe,STREAMING
  - DOMAIN-SUFFIX,youtube.ph,STREAMING
  - DOMAIN-SUFFIX,youtube.pk,STREAMING
  - DOMAIN-SUFFIX,youtube.pl,STREAMING
  - DOMAIN-SUFFIX,youtube.pr,STREAMING
  - DOMAIN-SUFFIX,youtube.pt,STREAMING
  - DOMAIN-SUFFIX,youtube.qa,STREAMING
  - DOMAIN-SUFFIX,youtube.ro,STREAMING
  - DOMAIN-SUFFIX,youtube.rs,STREAMING
  - DOMAIN-SUFFIX,youtube.ru,STREAMING
  - DOMAIN-SUFFIX,youtube.sa,STREAMING
  - DOMAIN-SUFFIX,youtube.se,STREAMING
  - DOMAIN-SUFFIX,youtube.sg,STREAMING
  - DOMAIN-SUFFIX,youtube.si,STREAMING
  - DOMAIN-SUFFIX,youtube.sk,STREAMING
  - DOMAIN-SUFFIX,youtube.sn,STREAMING
  - DOMAIN-SUFFIX,youtube.soy,STREAMING
  - DOMAIN-SUFFIX,youtube.sv,STREAMING
  - DOMAIN-SUFFIX,youtube.tn,STREAMING
  - DOMAIN-SUFFIX,youtube.tv,STREAMING
  - DOMAIN-SUFFIX,youtube.ua,STREAMING
  - DOMAIN-SUFFIX,youtube.ug,STREAMING
  - DOMAIN-SUFFIX,youtube.uy,STREAMING
  - DOMAIN-SUFFIX,youtube.vn,STREAMING
  - DOMAIN-SUFFIX,youtubeeducation.com,STREAMING
  - DOMAIN-SUFFIX,youtubefanfest.com,STREAMING
  - DOMAIN-SUFFIX,youtubegaming.com,STREAMING
  - DOMAIN-SUFFIX,youtubego.co.id,STREAMING
  - DOMAIN-SUFFIX,youtubego.co.in,STREAMING
  - DOMAIN-SUFFIX,youtubego.com,STREAMING
  - DOMAIN-SUFFIX,youtubego.com.br,STREAMING
  - DOMAIN-SUFFIX,youtubego.id,STREAMING
  - DOMAIN-SUFFIX,youtubego.in,STREAMING
  - DOMAIN-SUFFIX,youtubei.googleapis.com,STREAMING
  - DOMAIN-SUFFIX,youtubekids.com,STREAMING
  - DOMAIN-SUFFIX,youtubemobilesupport.com,STREAMING
  - DOMAIN-SUFFIX,yt.be,STREAMING
  - DOMAIN-SUFFIX,ytimg.com,STREAMING
  # tiktok
  - DOMAIN-SUFFIX,byteoversea.com,STREAMING
  - DOMAIN-SUFFIX,ibytedtos.com,STREAMING
  - DOMAIN-SUFFIX,muscdn.com,STREAMING
  - DOMAIN-SUFFIX,musical.ly,STREAMING
  - DOMAIN-SUFFIX,tiktok.com,STREAMING
  - DOMAIN-SUFFIX,tik-tokapi.com,STREAMING
  - DOMAIN-SUFFIX,tiktokcdn.com,STREAMING
  - DOMAIN-SUFFIX,tiktokv.com,STREAMING
  - DOMAIN-KEYWORD,-tiktokcdn-com,STREAMING
  # Game
  - DOMAIN-SUFFIX,garena.com,GAME
  - DOMAIN-SUFFIX,pubgmobile.com,GAME
  # Zerotier
  - DOMAIN,my.zerotier.com,ZEROTIER
  - DOMAIN-SUFFIX,zerotier.com,ZEROTIER
  - DST-PORT,9993,GAME
  - IP-CIDR,84.17.53.155/23,ZEROTIER
  - IP-CIDR,103.195.103.66/23,ZEROTIER
  - IP-CIDR,50.7.252.138/23,ZEROTIER
  - IP-CIDR,104.194.8.134/23,ZEROTIER
  - DOMAIN-SUFFIX,zerotier.com,ZEROTIER
  # FreeFire
  - DOMAIN-KEYWORD,freefire,GAME
  - DOMAIN-SUFFIX,garena.com,GAME
  - DOMAIN-SUFFIX,avatargarenanow-a.akamaihd.net,GAME
  - DOMAIN-SUFFIX,cdngarenanow-a.akamaihd.net,GAME
  - DOMAIN-SUFFIX,dlmobilegarena-a.akamaihd.net,GAME
  - DOMAIN-SUFFIX,garena.co.id,GAME
  - DOMAIN-SUFFIX,garena.co.th,GAME
  - DOMAIN-SUFFIX,garena.live,GAME
  - DOMAIN-SUFFIX,garena.my,GAME
  - DOMAIN-SUFFIX,garena.ph,GAME
  - DOMAIN-SUFFIX,garena.sg,GAME
  - DOMAIN-SUFFIX,garena.tv,GAME
  - DOMAIN-SUFFIX,garena.tw,GAME
  - DOMAIN-SUFFIX,garena.vn,GAME
  - DOMAIN-SUFFIX,garenanow.com,GAME
  - DOMAIN-SUFFIX,seagroup.com,GAME
  # PUBG
  - DOMAIN-SUFFIX,pubgmobile.com,GAME
  - DOMAIN-SUFFIX,igamecj.com,GAME
  - DOMAIN,file-igamecj.akamaized.net,GAME
  - IP-CIDR,45.40.220.0/22,GAME
  - IP-CIDR,150.109.124.0/23,GAME
  - IP-CIDR,49.51.228.0/23,GAME
  - IP-CIDR,170.106.102.0/24,GAME
  # Hotstar
  - IP-CIDR,192.168.1.1/24,STREAMING
  # tv
  - DOMAIN-SUFFIX,av-live-cdn.mncnow.id,STREAMING
  - DOMAIN-SUFFIX,bangjaxtv.blogspot.com,STREAMING
  # Disney+
  - DOMAIN-KEYWORD,hotstar,STREAMING
  - DOMAIN-SUFFIX,hotstar.com,STREAMING
  - DOMAIN-SUFFIX,expressplay.com,STREAMING
  - DOMAIN-SUFFIX,measurement.com,STREAMING
  - DOMAIN-SUFFIX,bamgrid.com,STREAMING
  - DOMAIN-SUFFIX,disneyplus.com,STREAMING
  - DOMAIN-SUFFIX,disney-plus.net,STREAMING
  - DOMAIN-SUFFIX,disneystreaming.com,STREAMING
  - DOMAIN-SUFFIX,dssott.com,STREAMING
  - DOMAIN,cdn.registerdisney.go.com,STREAMING
  # Vidio
  - DOMAIN-SUFFIX,thumbor.prod.vid.id,VIDIO
  - DOMAIN-SUFFIX,static-playback.prod.vid.id,VIDIO
  - DOMAIN-SUFFIX,vid.id,VIDIO
  - DOMAIN-SUFFIX,static-playback-vidio-com.akamaized.net,VIDIO
  - DOMAIN-SUFFIX,plenty.vidio.com,VIDIO
  - DOMAIN-SUFFIX,vidio.com,VIDIO
  - DOMAIN-SUFFIX,www.vidio.com,VIDIO
  - DOMAIN-SUFFIX,api.vidio.com,VIDIO
  - DOMAIN-SUFFIX,api-ns.vidio.com,VIDIO
  - DOMAIN-SUFFIX,media-vidio-com.akamaized.net,VIDIO
  - DOMAIN-SUFFIX,static-web-prod-vidio.akamaized.net,VIDIO
  - DOMAIN-SUFFIX,geo-id-media-vidio-com.akamaized.net,VIDIO
  - DOMAIN-SUFFIX,hermes.vidio.com,VIDIO
  - DOMAIN-SUFFIX,token-media-vidio-com.akamaized.net,VIDIO
  - DOMAIN-SUFFIX,etslive-2-vidio-com.akamaized.net,VIDIO
  - DOMAIN-SUFFIX,live-production.secureswiftcontent.com,VIDIO
  - DOMAIN-SUFFIX,secureswiftcontent.com,VIDIO
  - DOMAIN-SUFFIX,vidiocdn.com,VIDIO
  - DOMAIN-KEYWORD,vidio,VIDIO
  # bstation
  - DOMAIN-SUFFIX,m.bstation.com,VIDIO
  - DOMAIN-SUFFIX,bevent.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,bmeta.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,bkol.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,bogv.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,bsns.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,bugc.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,test456.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,www.bilibili.tv,VIDIO
  - DOMAIN-SUFFIX,www.bstation.com,VIDIO
  - DOMAIN-SUFFIX,bstation.com,VIDIO
  - DOMAIN-SUFFIX,bilivideo.com,VIDIO
  - DOMAIN-SUFFIX,xlaxiata2.md-apis.medallia.com,VIDIO
  # bokep
  - DOMAIN-SUFFIX,phncdn.com,BOKEP
  - DOMAIN-SUFFIX,phprcdn.com,BOKEP
  - DOMAIN-SUFFIX,porngub.com,BOKEP
  - DOMAIN-SUFFIX,pornhub-deutsch.net,BOKEP
  - DOMAIN-SUFFIX,pornhubapparel.com,BOKEP
  - DOMAIN-SUFFIX,pornhub.com,BOKEP
  - DOMAIN-SUFFIX,pornhub.org,BOKEP
  - DOMAIN-SUFFIX,pornhubpremium.com,BOKEP
  - DOMAIN-SUFFIX,phncdn.com,BOKEP
  - DOMAIN-SUFFIX,phprcdn.com,BOKEP
  - DOMAIN-SUFFIX,pornhub.com,BOKEP
  - DOMAIN-SUFFIX,pornhubpremium.com,BOKEP

  - IP-CIDR,127.0.0.0/8,DIRECT
  - GEOIP,CN,DIRECT
  - DST-PORT,80,DIRECT
  - SRC-PORT,7777,DIRECT
  - RULE-SET,LAN,DIRECT,no-resolve
  - MATCH,FINAL 