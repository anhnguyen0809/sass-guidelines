
# 반응형 웹 디자인과 브레이크포인트

반응형 웹 디자인은 이제 어디에서나 볼 수 있는 만큼 따로 소개해야 한다고 생각하진 않습니다. *Sass 스타일가이드에 왜 RWD 섹션이 있는 거야?*라고 자문하실지도 모르겠습니다. 사실 브레이크포인트의 사용을 쉽게 만들기 위해 할 수 있는 일들이 꽤 있고, 그래서 여기에 포함시키는 게 그리 나쁜 아이디어는 아닐 거라 생각했습니다.

## 브레이크포인트 이름 짓기

미디어 쿼리가 특정 기기에 의존해서는 안된다고 말해도 과언은 아닐 거라 생각합니다. 예를 들면, 아이패드나 블랙베리 폰을 특정해서 겨냥하는 것은 분명 나쁜 생각입니다. 디자인이 깨지고 다음 미디어 쿼리가 넘겨받기 전까지, 미디어 쿼리는 다양한 스크린 크기를 처리해야 합니다.

같은 이유로, 브레이크포인트는 기기의 이름이 아니라 보다 보편적인 것을 따라서 이름 지어져야 합니다. 특히 몇몇 폰은 이제 태블릿보다 크고, 몇몇 태블릿은 일부 작은 스크린의 컴퓨터보다 크기 때문입니다.

{% include snippets/rwd/01/index.html %}

이런 견지에서 볼 때, 디자인이 특정 기기에 직접적으로 관련되지 않았다는 것을 명확히 밝히는 어떤 작명 관례도 괜찮습니다. 크기에 대한 감을 전해줄 수 있기만 하면 됩니다.

{% include snippets/rwd/02/index.html %}

<div class="note">
  <p>앞의 예시들은 브레이크포인트를 정의하기 위해 맵을 중첩해서 사용하고 있지만, 이건 여러분이 어떤 브레이크포인트 매니저를 사용하는가에 전적으로 달렸습니다. 유연성을 위해 맵을 포개어넣는 대신 문자열을 선택할 수도 있을 겁니다. (예를 들면 <code>'(min-width: 800px)'</code>).</p>
</div>

###### 참고

* [Naming Media Queries](http://css-tricks.com/naming-media-queries/)

## 브레이크포인트 매니저

일단 원하는 방식으로 브레이크포인트의 이름을 짓고 나면, 실제 미디어쿼리에서 사용할 방법이 필요합니다. 많은 방법들이 있지만 전 getter 함수로 읽을 수 있는 브레이크포인트 맵의 열혈 팬이라는 것을 밝혀야겠습니다. 이 시스템은 간단하면서도 효과적입니다.

{% include snippets/rwd/03/index.html %}

<div class="note">
  <p>확실히, 이건 아주 단순한 브레이크포인트 매니저입니다. 좀 더 많은 기능을 제공하는 브레이크포인트 매니저가 필요하다면, 바퀴를 새로 발명할 것 없이 <a href="https://github.com/sass-mq/sass-mq">Sass-MQ</a>, <a href="http://breakpoint-sass.com/">Breakpoint</a>, <a href="https://github.com/eduardoboucas/include-media">include-media</a>와 같은 효과가 검증된 것을 사용하기를 권합니다.</p>
</div>

###### 참고

* [Managing Responsive Breakpoints in Sass](http://www.sitepoint.com/managing-responsive-breakpoints-sass/)
* [Approaches to Media Queries in Sass](http://css-tricks.com/approaches-media-queries-sass/)

## 미디어 쿼리 사용법

얼마 전, 미디어 쿼리를 어디에 작성해야 하는지에 대한 치열한 논쟁이 있었습니다: 선택자 안으로 들어가야 하는가(Sass에서는 가능하므로), 아니면 철저하게 분리해야 하는가? 저는 *선택자-속-미디어-쿼리* 시스템의 열렬한 옹호자라는 점을 밝혀야겠습니다. 그 쪽이 *컴퍼넌트* 아이디어와 잘 어울린다고 생각하거든요.

{% include snippets/rwd/04/index.html %}

위의 코드는 다음의 CSS를 만들어냅니다:

{% include snippets/rwd/05/index.html %}

이 방식은 미디어 쿼리의 중복을 야기한다는 말을 들으실지도 모릅니다. 그것은 분명한 사실입니다. 그러나, 실험에 따르면 Gzip(혹은 그에 상당하는 것) 이후에는 문제가 되지 않습니다.

> … 우리는 미디어 쿼리를 한 곳에 몰아넣는 것 혹은 산발적으로 배치하는 것이 성능에 영향을 미치는지에 대한 논의를 이어갔고, 압축 시, 최악의 경우 미세한 차이가 존재하며, 최선의 경우 기본적으로 차이가 존재하지 않는다는 결론에 이르렀다.<br>
> &mdash; [Sam Richards](https://twitter.com/snugug), [Breakpoint](http://breakpoint-sass.com/)에 관해

정말로 미디어 쿼리의 중복이 신경쓰인다면, [이 gem](https://github.com/aaronjensen/sass-media_query_combiner)과 같은 도구를 이용해 합칠 수 있습니다. 하지만 CSS 코드를 옮길 때 발생할 수 있는 부작용에 대해 경고해야 할 것 같습니다. 여러분은 소스의 순서가 중요하다는 사실을 잘 알고 있습니다.

###### 참고

* [Inline or Combined Media queries? Fight!](http://benfrain.com/inline-or-combined-media-queries-in-sass-fight/)
* [Sass::MediaQueryCombiner](https://github.com/aaronjensen/sass-media_query_combiner)
