# nextcloud

if NEXTCLOUD_TRUSTED_DOMAINS doesnt work, setup at `config.php`:
```php
'trusted_domains' => 
  array (
    0 => 'localhost',
  ),
```

#### Modify each page
- example: loop video player
```bash
docker cp nextcloud:/var/www/html/core/templates/layout.user.php ./layout.user.php 
nano layout.user.php 
```
```html
<script nonce="<?php p($_['cspNonce']);?>">
  const setLoopOnVideos = () => {
    document.querySelectorAll("video").forEach(video => {
      if (!video.hasAttribute("loop")) {
        video.setAttribute("loop", "true");
        console.log(`Video ${video.src} set to loop`);
      }
    });
  };

  setLoopOnVideos();

  new MutationObserver(setLoopOnVideos).observe(document.body, {
    childList: true,
    subtree: true
  });
</script>
```
```bash
docker cp ./layout.user.php nextcloud:/var/www/html/core/templates/layout.user.php
docker restart nextcloud
```
