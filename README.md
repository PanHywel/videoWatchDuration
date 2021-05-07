# videoWatchDuration

Time statistics, remove SEEK time and add a multiplier statistics

```javascript
const video = document.querySelector("video");
const watchMaxDurationCountData = {
  flag: false,
  speedValue: 1000,
  timer: null,
  watchMaxDuration: 0,
};

function watchMaxDurationCount() {
  if (watchMaxDurationCountData.flag) {
    if (watchMaxDurationCountData.timer) {
      clearInterval(watchMaxDurationCountData.timer);
      watchMaxDurationCountData.timer = null;
    }
    watchMaxDurationCountData.timer = setInterval(() => {
      watchMaxDurationCountData.speedValue = 1 * video.playbackRate;
      if (!watchMaxDurationCountData.flag && watchMaxDurationCountData.timer) {
        clearInterval(watchMaxDurationCountData.timer);
        watchMaxDurationCountData.timer = null;
      }
      watchMaxDurationCountData.watchMaxDuration +=
        watchMaxDurationCountData.speedValue;
      document.querySelector("#duration").innerText =
        watchMaxDurationCountData.watchMaxDuration;
    }, 1000);
  }
}

video.addEventListener("play", function (e) {
  watchMaxDurationCountData.flag = true;
  watchMaxDurationCountData.speedValue = 1 * video.playbackRate;
  watchMaxDurationCount();
});
video.addEventListener("ended", function (e) {
  watchMaxDurationCountData.flag = false;
});
video.addEventListener("pause", function (e) {
  watchMaxDurationCountData.flag = false;
});

function setPlaybackRate(value) {
  video.playbackRate = value;
}
```
