<!--
template: home
title: G2
keywords:
  - G2
  - The Grammar of Graphics
  - 图形语法
featuresCards:
  - img: ${assets}/image/home/features-simple.svg
    title: 简单方便
    description: 从数据出发，仅需几行代码可以轻松获得想要的图表展示效果。
  - img: ${assets}/image/home/features-professional.svg
    title: 完备的编码
    description: 大量产品实践之上，提供绘图引擎。完备图形语法，专业设计规范。
  - img: ${assets}/image/home/features-powerful.svg
    title: 强大扩展能力
    description: 任何图表，都可以基于图形语法灵活绘制，满足你无限的创意。
footer:
  isDark: true
resource:
  jsFiles:
    - ${url.g2}
    - ${url.dataSet}
-->

<section class="intro">
    <div class="container">
        <div class="header row">
            <div class="col-md-6">
                <h1>G2基础图表类库</h1>
                <p class="main-info">是一个由纯 JavaScript 编写、强大的语义化图表生成工具，它提供了一整套图形语法，支持多种坐标系绘制，可以让用户自由地定制图表。</p>
                <a href="{{ products.g2.links.demo.href }}" class="btn btn-primary btn-lg">{{ resource.translate.getStarted }}</a>
                <a href="{{base}}zh-cn/g2/3.x/tutorial/download.html" class="btn btn-light border btn-lg">{{ resource.translate.downloadAndUse }}</a>
            </div>
            <div class="col-md-6 slick">
                <div id="commentsCarousel" class="carousel">
                    <div class="carousel-inner slick">
                        <div id="c1" class="carousel-item active"></div>
                        <div id="c2" class="carousel-item"></div>
                        <div id="c3" class="carousel-item"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>

<section class="features text-center">
    <div class="container">
        <div class="row">
            {% for card in featuresCards %}
            <div class="feature col-md-4 text-center">
                <img src="{{ card.img }}" alt="" width="120" height="120">
                <h5>{{ card.title }}</h5>
                <div class="detail">{{ card.description }}</div>
            </div>
            {% endfor %}
        </div>
    </div>
</section>

<section class="get-started text-center"><div class="container">
    <h2>快速接入</h2>
    <p>通过 <code>&lt;script&gt;</code> 标签引入：</p>

```html
<!-- 引入在线资源 -->
<script src="https://a.alipayobjects.com/g/datavis/g2/2.3.12/index.js"></script>
```

</div></section>

<section class="more text-center">
    <a href="{{ products.g2.links.tutorial.href }}" class="btn btn-primary btn-lg">更多教程</a>
</section>

<!-- chart1 -->

```js-
  var data = [
    { month: 'Jan', Tokyo: 7.0, London: 3.9 },
    { month: 'Feb', Tokyo: 6.9, London: 4.2 },
    { month: 'Mar', Tokyo: 9.5, London: 5.7 },
    { month: 'Apr', Tokyo: 14.5, London: 8.5 },
    { month: 'May', Tokyo: 18.4, London: 11.9 },
    { month: 'Jun', Tokyo: 21.5, London: 15.2 },
    { month: 'Jul', Tokyo: 25.2, London: 17.0 },
    { month: 'Aug', Tokyo: 26.5, London: 16.6 },
    { month: 'Sep', Tokyo: 23.3, London: 14.2 },
    { month: 'Oct', Tokyo: 18.3, London: 10.3 },
    { month: 'Nov', Tokyo: 13.9, London: 6.6 },
    { month: 'Dec', Tokyo: 9.6, London: 4.8 }
  ];
  var ds = new DataSet();
  var dv = ds.createView().source(data);
  dv.transform({
    type: 'fold',
    fields: [ 'Tokyo', 'London' ], // 展开字段集
    key: 'city', // key字段
    value: 'temperature', // value字段
  });
  var chart = new G2.Chart({
    container: 'c1',
    forceFit: true,
    height: 400
  });
  chart.source(dv, {
    month: {
      range: [ 0, 1 ]
    }
  });
  chart.tooltip({
    crosshairs: {
      type: 'line'
    }
  });
  chart.axis('temperature', {
    label: {
      formatter: val => {
        return val + '°C';
      }
    }
  });
  chart.line().position('month*temperature').color('city').size(2).shape('smooth');
  chart.point().position('month*temperature').color('city').size(4).shape('circle').style({
    stroke: '#fff',
    lineWidth: 1
  });
  chart.render();
```

<!-- chart2 -->

```js-
  const data = [
    { name:'London', 'Jan.': 18.9, 'Feb.': 28.8, 'Mar.' :39.3, 'Apr.': 81.4, 'May': 47, 'Jun.': 20.3, 'Jul.': 24, 'Aug.': 35.6 },
    { name:'Berlin', 'Jan.': 12.4, 'Feb.': 23.2, 'Mar.' :34.5, 'Apr.': 99.7, 'May': 52.6, 'Jun.': 35.5, 'Jul.': 37.4, 'Aug.': 42.4}
  ];
  const ds = new DataSet();
  const dv = ds.createView().source(data);
  dv.transform({
    type: 'fold',
    fields: [ 'Jan.','Feb.','Mar.','Apr.','May','Jun.','Jul.','Aug.' ], // 展开字段集
    key: '月份', // key字段
    value: '月均降雨量', // value字段
  });

  const chart = new G2.Chart({
    container: 'c2',
    forceFit: true,
    height: 400
  });
  chart.source(dv);
  chart.interval().position('月份*月均降雨量').color('name').adjust([{
    type: 'dodge',
    marginRatio: 1 / 32
  }]);
  chart.render();
```

<!-- chart3 -->

```js-
  var data = [
    {country: 'Asia', year: '1750', value: 502},
    {country: 'Asia', year: '1800', value: 635},
    {country: 'Asia', year: '1850', value: 809},
    {country: 'Asia', year: '1900', value: 5268},
    {country: 'Asia', year: '1950', value: 4400},
    {country: 'Asia', year: '1999', value: 3634},
    {country: 'Asia', year: '2050', value: 947},
    {country: 'Africa', year: '1750', value: 106},
    {country: 'Africa', year: '1800', value: 107},
    {country: 'Africa', year: '1850', value: 111},
    {country: 'Africa', year: '1900', value: 1766},
    {country: 'Africa', year: '1950', value: 221},
    {country: 'Africa', year: '1999', value: 767},
    {country: 'Africa', year: '2050', value: 133},
    {country: 'Europe', year: '1750', value: 163},
    {country: 'Europe', year: '1800', value: 203},
    {country: 'Europe', year: '1850', value: 276},
    {country: 'Europe', year: '1900', value: 628},
    {country: 'Europe', year: '1950', value: 547},
    {country: 'Europe', year: '1999', value: 729},
    {country: 'Europe', year: '2050', value: 408},
    {country: 'Oceania', year: '1750', value: 200},
    {country: 'Oceania', year: '1800', value: 200},
    {country: 'Oceania', year: '1850', value: 200},
    {country: 'Oceania', year: '1900', value: 460},
    {country: 'Oceania', year: '1950', value: 230},
    {country: 'Oceania', year: '1999', value: 300},
    {country: 'Oceania', year: '2050', value: 300},
  ];
  const chart = new G2.Chart({
    container: 'c3',
    forceFit: true,
    height: 400
  });
  chart.source(data, {
    year: {
      type: 'linear',
      tickInterval: 50
    }
  });
  chart.tooltip({
    crosshairs: {
      type: 'line'
    }
  });
  chart.areaStack().position('year*value').color('country');
  chart.lineStack().position('year*value').color('country').size(2);
  chart.render();
```