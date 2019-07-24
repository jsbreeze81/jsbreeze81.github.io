---
layout: post
title: "YouTube API"
author: "2019-07-24"
---

2019.07.24 기준 YouTube API 옵션, 함수 정리 (javascript)

# Youtube API load

{% highlight js %}
// loads youtube API script
var tag = document.createElement('script');    
tag.src = "https://www.youtube.com/iframe_api";
var firstScriptTag = document.getElementsByTagName('script')[0];
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
{% endhighlight %}

# 기본구조

{% highlight js %}
function onYouTubeIframeAPIReady() {
    player = new YT.Player('player id', {
        height: '360',
        width: '640',
        videoId: 'video id',
        playerVars:{ //options
            'autoplay': 1, //자동재생 : 0(default), 1
            'controls' : 1, //컨트롤러 표시 : 0, 1(default), 2
            'enablejsapi' : 1, //javascript API 사용하도록 설정 : 0(default), 1
            'loop' : 1, //반복재생(playlist 옵션과 함께 사용해야 동작) : 0(default), 1
            'playlist' : 'M7lc1UVf-VE', //재생할 영상 리스트 ID 
            'rel' : 0, // 동영상 종료 후 관련영상 표시여부 설정 : 0, 1(default)
            'showinfo' : 0, //영상관련 정보 표시 : 0, 1(default)
            'playsinline' : 0 //iso에서 전체화면 or 인라인으로 재생여부 설정 : 0(default), 1
        },
        events: {
            /*
            'onReady': onPlayerReady, // 플레이어 로드가 완료되면 호출
            'onStateChange': onPlayerStateChange, // 플레이어 상태가 변경되면 호출
                            // 6가지 상태값
                            // -1 : 시작되지않음
                            // 0 or YT.PLayerState.ENDED : 종료
                            // 1 or YT.PLayerState.PLAYING : 재생중
                            // 2 or YT.PLayerState.PAUSED : 일시중지됨
                            // 3 or YT.PLayerState.BUFFERING : 버퍼링 중
                            // 5 or YT.PLayerState.CUED : 동영상 신호
            'onError' : onErrorCode // 플레이어에서 오류 발생하면 호출
                            // 5가지 상태값
                            // 2 : 잘못된 매개변수 값 포함
                            // 5 : HTML5 플레이어와 관련된 오류
                            // 100 : 동영상을 찾을 수 없는 경우(삭제, 비공개)
                            // 101, 150 : 동영상 소유자가 내장 플레이어에서 동영상 재생하는 것을 혀용하지 않음
            */
        }
    });
}
{% endhighlight %}

# 함수
## 1) 재생
{% highlight js %}
player.playVideo(); // 재생
player.pauseVideo(); // 일시정지
player.stopVideo(); // 정지
player.seekTo(seconds:Number, allowSeekAhead:Boolean); // 지정 시간으로 이동
{% endhighlight %}

## 2) 재생목록
{% highlight js %}
player.nextVideo(); // 재생목록 다음 영상 재생
player.previousVideo(); // 재생목록 이전 영상 재생
player.playVideoAt(index:Number); // 재생목록 이전 영상 재생
{% endhighlight %}

## 3) 볼륨
{% highlight js %}
player.mute(); // 음소거
player.unMute(); // 음소거 해제
player.isMuted(); // 음소거 상태 반환 : 음소거 - true, 음소거X - false
player.setVolume(volume:Number); // 볼륨 설정 (0 ~ 100)
player.getVolume(); // 볼륨값 반환
{% endhighlight %}

## 4) 플레이어 크기 조정
{% highlight js %}
player.setSize(width:Number, height:Number)
{% endhighlight %}

## 5) 재생속도
{% highlight js %}
player.getPlaybackRate() // 재생속도 반환 (0.25, 0.5, 1, 1.5, 2, ...)
{% endhighlight %}

## 6) 플레이 리스트
{% highlight js %}
player.setLoop(loopPlaylists:Boolean); // play list 연속재생 여부 세팅
player.setShuffle(shufflePlaylist:Boolean); // play list 무작위 재생
{% endhighlight %}

## 7) 상태
{% highlight js %}
player.getPlayerState(); // 플레이어 상태값 반환
                        // 6가지 상태값
                        // -1 : 시작되지않음
                        // 0 : 종료
                        // 1 : 재생중
                        // 2 : 일시중지됨
                        // 3 : 버퍼링 중
                        // 5 : 동영상 신호
player.getCurrentTime(); // 재생시간 초 단위로 반환
{% endhighlight %}

## 8) 동영상 정보
{% highlight js %}
player.getDuration(); // 전체 재생시간을 초단위로 반환, 동영상 재생이 시작된 직후 발생
player.getVideoUrl(); // 로드되었거나 재생중인 영상의 youtube url 반환
player.getVideoEmbedCode(); // 로드되었거나 재생중인 영상의 삽입코드 반환
{% endhighlight %}

## 9) 이벤트 리스너
{% highlight js %}
player.addEventListener(event:String, listener:String); //이벤트 리스너 추가
player.removeEventListener(event:String, listener:String); //이벤트 리스너 삭제
{% endhighlight %}

## 10) DOM노드 제어
{% highlight js %}
player.getIframe(); // iframe DOM노드 반환
player.destroy(); // iframe 삭제
{% endhighlight %}

# 2개이상 영상 로드할 경우
{% highlight js %}
// player, video info
var playList = [
    {elId:"player1", videoId:"M7lc1UVf-VE"},
    {elId:"player2", videoId:"M7lc1UVf-VE"}
];

// player
var players = new Array();

function onYouTubeIframeAPIReady() {
    if(playList.length == 0) return;

    for(var i=0; i<playList.length; i++){
        players[i] = new YT.Player(playList[i].elId, {
            height: '360',
            width: '640',
            videoId: playList[i].videoId,
            playerVars:{ ... },
            events: { ... }
        });
    }
}
{% endhighlight %}


_The end_
