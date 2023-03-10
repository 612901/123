# ð¦ ç¨åºé¨ç½²

## Docker é¨ç½²

æ¨èä½¿ç¨ Docker é¨ç½²ï¼éé¢åå®è£ [Docker å¼æ](https://docs.docker.com/engine/install/)ï¼æå¡å¨æ§è¡å½ä»¤åå»ºå®¹å¨ï¼

```bash
docker run -d \
    --name artalk \
    -p 8080:23366 \
    -v $(pwd)/data:/data \
    artalk/artalk-go
```

> åè®¾åå `http://your_domain` å·²æ­£ç¡®æ·»å  DNS è®°å½å¹¶æåä½ çæå¡å¨ IP

æµè§å¨æå¼ `http://your_domain:8080` å°åºç° Artalk åå°ç»éçé¢ã

æ§è¡å½ä»¤åå»ºç®¡çåè´¦æ·ï¼

```bash
docker exec -it artalk artalk admin
```

å¨ä½ çç½ç«å¼å¥ Artalk ç¨åºååµççåç«¯ CSSãJS èµæºå¹¶åå§åï¼

> æ³¨ï¼å° `http://your_domain:8080` æ¹ä¸ºä½ çæå¡å¨ååï¼æä½¿ç¨ [å¬å± CDN èµæº](#cdn-èµæº)ã

```html
<!-- CSS -->
<link href="http://your_domain:8080/dist/Artalk.css" rel="stylesheet">

<!-- JS -->
<script src="http://your_domain:8080/dist/Artalk.js"></script>

<!-- Artalk -->
<div id="Comments"></div>
<script>
new Artalk({
  el:        '#Comments',                // ç»å®åç´ ç Selector
  pageKey:   '/post/1',                  // åºå®é¾æ¥ (çç©ºèªå¨è·å)
  pageTitle: 'å³äºå¼å¥ Artalk çè¿æ¡£å­äº',  // é¡µé¢æ é¢ (çç©ºèªå¨è·å)
  server:    'http://your_domain:8080',  // åç«¯å°å
  site:      'Artalk çåå®¢',             // ä½ çç«ç¹å
})
</script>
```

å¨è¯è®ºæ¡è¾å¥ç®¡çåçç¨æ·ååé®ç®±ï¼æ§å¶å°å¥å£æé®å°åºç°å¨è¯è®ºæ¡å³ä¸è§ä½ç½®ã

å¨æ§å¶å°ï¼ä½ å¯ä»¥æ ¹æ®åå¥½éç½®è¯è®ºç³»ç»ã[å°è¯è®ºè¿ç§»å° Artalk](./transfer.md)ã

ç¥è´ºï¼ä½ å·²æåå®æ Artalk é¨ç½² ð¥³

## æ®éæ¹å¼é¨ç½²

1. åå¾ [GitHub Release](https://github.com/ArtalkJS/Artalk/releases) ä¸è½½ç¨åºåç¼©å
2. æååç¼©åï¼`tar -zxvf artalk_çæ¬å·_ç³»ç»_æ¶æ.tar.gz`
3. è¿è¡ç¨åº `./artalk server`
4. åç«¯éç½®

    ```js
    new Artalk({ server: "http://your_domain:23366" })
    ```

**å¶å®å¯éæä½ï¼**

- [âååä»£çç«¯å£å° 80 / 443 (Nginx, Apache)â](/guide/backend/reverse-proxy.md)
- ["æä¹åè¿ä½ (tmux, systemd, supervisor)"](/guide/backend/daemon.md)

**éè¡¨ï¼æä»¶åéä¹è¡¨**

|æä»¶å|æä½ç³»ç»|CPU æ¶æ|
|:-|:-:|:-:|
|artalk_linux_amd64.tar.gz|Linux|x86_64|
|artalk_linux_arm64.tar.gz|Linux|ARM64|
|artalk_linux_arm7.tar.gz|Linux|ARMv7|
|artalk_windows_amd64.zip|Windows|x86_64|
|artalk_darwin_arm64.tar.gz|macOS|Apple Silicon|
|artalk_darwin_amd64.tar.gz|macOS|Intel Chip <sup>~~(ä»ä¹çå±)~~</sup>|

## Docker Compose é¨ç½²

æä¾ docker-compose.yaml æä»¶å¯ä¾åèï¼

```yaml
version: "3.5"
services:
  artalk:
    container_name: artalk
    image: artalk/artalk-go
    ports:
      - 8080:23366
    volumes:
      - ./data:/data
```

å¨ä¸éç½®æä»¶ç¸åçç®å½æ§è¡å½ä»¤åå»ºå®¹å¨ï¼

```bash
docker-compose up -d
```

::: details ä¸äº Docker Compose å¸¸ç¨å½ä»¤

```bash
docker-compose restart  # éå¯å®¹å¨
docker-compose stop     # æåå®¹å¨
docker-compose down     # å é¤å®¹å¨
docker-compose pull     # æ´æ°éå
docker-compose exec artalk bash # è¿å¥å®¹å¨
```

:::

> è¯¦ç»å¯è§ï¼[âåç«¯ Â· Dockerâ](/guide/backend/docker.md)

## èªè¡ç¼è¯å¹¶è¿è¡

å¯åèï¼[âåç«¯æå»ºâ](./backend/build.md)

## CDN èµæº

::: tip Artalk ææ°çæ¬

å½å Artalk åç«¯ææ°çæ¬å·ä¸ºï¼ **:ArtalkVersion:**

è¥éåçº§åç«¯ï¼è¯·å° URL ä¸­ççæ¬å·æ°å­é¨åæ¿æ¢å³å¯ã
:::

Artalk åç«¯ç¨åºååµäºåç«¯ JSãCSS æä»¶ï¼ä½¿ç¨å¬å± CDN èµæºè¯·æ³¨æååç«¯çæ¬çå¼å®¹æ§ã

Artalk éæèµæºéè¿ä¸æ¸¸ [CDNJS](https://cdnjs.com/) ååï¼å½åæè®¸å¤éåå¯ä¾éæ©ï¼

**BootCDN (å½å)**

> https://cdn.bootcdn.net/ajax/libs/artalk/:ArtalkVersion:/Artalk.js
>
> https://cdn.bootcdn.net/ajax/libs/artalk/:ArtalkVersion:/Artalk.css


**ElemeCDN (å½å)**

> https://npm.elemecdn.com/artalk@:ArtalkVersion:/dist/Artalk.js
>
> https://npm.elemecdn.com/artalk@:ArtalkVersion:/dist/Artalk.css

**CDNJS**

> https://cdnjs.cloudflare.com/ajax/libs/artalk/:ArtalkVersion:/Artalk.js
>
> https://cdnjs.cloudflare.com/ajax/libs/artalk/:ArtalkVersion:/Artalk.css

**UNPKG**

> https://unpkg.com/artalk@:ArtalkVersion:/dist/Artalk.js
> 
> https://unpkg.com/artalk@:ArtalkVersion:/dist/Artalk.css

**JS DELIVR**

> https://cdn.jsdelivr.net/npm/artalk@:ArtalkVersion:/dist/Artalk.js
> 
> https://cdn.jsdelivr.net/npm/artalk@:ArtalkVersion:/dist/Artalk.css

## ArtalkLite

å¯éæ©ç²¾ç®ç [ArtalkLite](./frontend/artalk-lite.md)ï¼ä½ç§¯æ´å°ãæ´ç®çº¦ã

## Node ç¯å¢

```bash
pnpm add artalk
```

å¼å¥å°ä½ çé¡¹ç®ï¼

```js
import 'artalk/dist/Artalk.css'
import Artalk from 'artalk'

new Artalk({
  // ...
})
```

## ä½æ¶å¼å¥ãä½æ¶ newï¼

- å¯ä»¥å¨ä»»æä½ç½®å¼å¥ JS å CSS èµæºï¼ä½éç¡®ä¿ JS å¼å¥å¨æ§è¡ `new Artalk({})` åã
- æ§è¡ `new Artalk({ el: '#x' })` æ¶ï¼éè¦ç¡®ä¿ `<div id="x"></div>` å­å¨äºé¡µé¢å½ä¸­ã

å¯åèï¼[âåç«¯æ¡æ¶å¼å¥â](./frontend/import-framework.md) / [âåå®¢å¼å¥â](./frontend/import-blog.md)

## æ°æ®å¯¼å¥

ä»å¶ä»è¯è®ºç³»ç»å¯¼å¥æ°æ®ï¼[âæ°æ®è¿ç§»â](./transfer.md)
