---
layout: post
title: "Datepicker"
---

2019.07.24 기준 datepicker 옵션 정리

# load file

{% highlight html %}
<!-- css -->
<link rel="stylesheet" href="jquery-ui.min.css">

<!-- javascript -->
<script src="jquery.min.js"></script>
<script src="jquery-ui.min.js"></script>

<!-- sprite 이미지 -->
{% endhighlight %}

# 기본구조

{% highlight js %}
$(".datepicker").datepicker({
    monthNames: ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월'], //월표시
    dayNamesMin: ['일', '월', '화', '수', '목', '금', '토'], //요일표시
    dateFormat: "yy-mm-dd", //선택된 값 표시 포멧
    showMonthAfterYear: true, //년월 위치 변경
    yearSuffix: "년", //달력의 년도 부분 뒤에 붙는 텍스트
    showOn: "both",
        //button: 달력 버튼 노출, 버튼을 눌러야만 달력 표시
        //both: 달력 버튼 노출, 버튼을 누르거나 input을 클릭하면 달력 표시  
    buttonImage: "버튼 이미지 경로",
    changeYear: true, // 년도 변경
    monthNamesShort: ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월'], 
    // 년도 변경 셀렉트 박스 월표시
    changeMonth: true, // 월 변경
    minDate: "-1M", //오늘 이전 선택가능일 지정(-1D:하루전, -1M:한달전, -1Y:일년전)
    maxDate: "+1M" //오늘 이후 선택가능일 지정(+1D:하루후, -1M:한달후, -1Y:일년후)     
});
{% endhighlight %}