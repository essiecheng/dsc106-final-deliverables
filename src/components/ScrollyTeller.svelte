<script>
  import Scroller from '@sveltejs/svelte-scroller';
  import Map from './Map.svelte';
  import { geoMercator } from 'd3-geo';
  import Project3 from './Proj3.svelte';
  import Athlete from './Athlete.svelte';
  import Bubble from './SportsBubble.svelte';
  import Country from './Country.svelte';
  import HomeAdv from './HomeAdv.svelte';
  import Rising from './Rising.svelte';
  import archery from './risingData/archery.js';
  import badminton from './risingData/badminton.js';
  import boxing from './risingData/boxing.js';
  import canoecayak from './risingData/canoecayak.js';
  import cycling from './risingData/cycling.js';
  import fencing from './risingData/fencing.js';
  import handball from './risingData/handball.js';
  import hockey from './risingData/hockey.js';
  import judo from './risingData/judo.js';
  import pentathlon from './risingData/pentathlon.js';
  import shooting from './risingData/shooting.js';
  import softball from './risingData/softball.js';
  import tabletennis from './risingData/tabletennis.js';
  import taekwondo from './risingData/taekwondo.js';
  import tennis from './risingData/tennis.js';
  import triathlon from './risingData/triathlon.js';
  import weightlifting from './risingData/weightlifting.js';
  import wrestling from './risingData/wrestling.js';
  import Top5 from './Top5.svelte';

  let count, index, offset, progress;
  let width, height;
  let show = false;

  let geoJsonToFit = {
    type: 'FeatureCollection',
    features: [
      {
        type: 'Feature',
        geometry: {
          type: 'Point',
          coordinates: [1, 0],
        },
      },
      {
        type: 'Feature',
        geometry: {
          type: 'Point',
          coordinates: [0, 1],
        },
      },
    ],
  };

  $: projection = geoMercator().fitSize([width, height], geoJsonToFit);
</script>

<Scroller
  top={0.0}
  bottom={1}
  threshold={0.5}
  bind:count
  bind:index
  bind:offset
  bind:progress
>
  <div
    class="background"
    slot="background"
    bind:clientWidth={width}
    bind:clientHeight={height}
  >
    <section class="b1"></section>
  </div>

  <div class="foreground" slot="foreground">
    <section class="intro-page">
      <h1 class="title">United States in the Olympics</h1>
      <p>Kyla Park and Essie Cheng</p>
      <div class="box">
        <div class="inner">
          <span>Exploration Through Visualization</span>
        </div>
        <div class="inner">
          <span>Exploration Through Visualization</span>
        </div>
      </div>
      <h2 class="intro">
        What's the secret to success?
        <br />
        <br />
        The United States has won the most medals in every Summer Olympics since
        1996. Will they end up on top once more in the upcoming 2024 Paris Olympics?
        Get ready to hit the ground <span class="highlight">running</span>
        and <span class="highlight">jump</span> into the thrilling world of the
        Olympics. Using a dataset on the Summer Olympics from 1976-2008, we’ll
        <span class="highlight">tackle</span>
        the question of what has fueled the United States’s legacy of success and
        <span class="highlight">dive</span> into the dynamics of their
        dominance. Then we'll take a <span class="highlight">shot</span>
        at providing a recommendation on their key to continuous and long lasting
        Olympic success.
      </h2>

      <div class="olympic-logo"></div>
    </section>

    <section class="proj3">
      <h3>Data Exploration</h3>
      <p class="instructions">
        A comprehensive overview of the Olympics: click bar to drill down into
        further detail, click background to go back up. Select/deselect medal
        buttons to filter type of medal.
      </p>
      <Project3 />
      <p class="explanation1">
        No matter the sport or year, the United States frequently appears. They
        seem to consistently be a dominant force, and maybe even be the best in
        the world. A look at the overall medal tally can confirm if this is
        true. ↓
      </p>
    </section>

    <section class="top-countries">
      <h3>Country Medal Leaders</h3>
      <p class="instructions">
        The top 3 countries of all time: each point represents a medal won,
        hover over points for more details
      </p>
      <Country />
      <p class="explanation2">
        Team USA is indeed a dominant force in the Olympics, winning the most
        medals out of all countries. What puts the U.S. on top of all others
        though? It is known teams generally have a home court advantage in
        sports... can that be applied to a larger scale of the Olympics? ↓
      </p>
    </section>

    <section class="home-advantage-1">
      <h3>Home Advantage</h3>
      <p class="instructions">
        Medal count history for each country that has hosted the Olympics: use
        dropdown menu to select location. Red dot indicates that the country
        hosted the Olympics that year
      </p>
      <HomeAdv />
      <p class="explanation1">
        It looks like home advantage could possibly exist. For many countries,
        their best performing year is when the year they host, or there's a drop
        in medal count the year after they host. The U.S. seems less affected by
        home advantage however. When they hosted 1984, their medal count is
        inflated due to the fact that the Soviet Union and other socialist
        countries declined to attend for political reasons. The Soviet Union,
        previously the United State's biggest competition, essentially cleared
        the way for the U.S. to dominate. The U.S. hosted again in 1996, but
        their top medal counts don't come from that year. Nonetheless, there is
        possible evidence of home advantage contributing to greater success for
        a country for that year. Additionally, the U.S. has hosted twices
        whereas other countries have hosted just once. What if the extra home
        advantage is what fuels its continuous dominance? Can home advantage be
        extended past success during the hosting year to overall long term
        success? ↓
      </p>
    </section>

    <section class="home-advantage-2">
      <h3>Home Advantage</h3>
      <p class="instructions">
        A broader look at the connection between home advantage and overall
        Olympic success: light blue countries have hosted the Olympics and are
        in the top ten for number of medals won overall. Purple countries have
        hosted the Olympics but are not in the top ten. Orange countries have
        not hosted the Olympics but are in the top ten. Hover the markers for
        host city and year.
      </p>
      <Map bind:geoJsonToFit {index} />
      <p class="explanation3">
        Out of the top 10 most winning countries, only 4 of them have hosted an
        Olympics. The other 4 countries that have hosted an Olympics aren't in
        the top 10. Therefore, there doesn't seem to be much of an advantage to
        hosting the Olympics when it comes to long term consistent success. This
        makes sense as the world's greatest athletes on the world’s greatest
        sporting stage are expected to perform well no matter the location or
        amount of support. What puts the U.S. above others then? Perhaps they're
        not only a jack of all trades, but a master of some too. ↓
      </p>
    </section>

    <section class="top-sports">
      <h3>Team USA Best Performing Sports</h3>
      <p class="instructions">
        Top 5 sports for Team USA each year: scroll through slider to change
        between years or click button for automated transitions.
      </p>
      <Bubble />
      <p class="explanation4">
        Team USA is noticably a powerhouse in aquatics and athletics. They have
        performed best in those two sports in every single Olympics, racking up
        countless medals in those areas. In fact, more than half its golds come
        from those 2 sports. Thus, what seems to be driving Team USA's high
        medal counts is being exceptionally good in certain sports, which allows
        them to dominate and snatch up medals. What's behind the phenomenal
        success in those sports though? ↓
      </p>
    </section>

    <section class="top-athletes">
      <h3>Top Olympic Athletes</h3>
      <p class="instructions">
        Top 3 Olympic athletes of all time: click the button to reveal each
        athlete. Then scroll the timeline on the right for more details about
        their feats.
      </p>
      <Athlete />
    </section>

    <section class="transition-section">
      <p class="explanation5">
        Of the top 3 athletes in the history of the Olympics, 2 of them are from
        Team USA and earned their medals in aquatics, aligning with the fact
        that Team USA’s best sport is aquatics. This indicates that consistent
        dominance in sports can be linked to superstar athletes who consistently
        perform well. The extraordinary athlete is what pushes the team above
        the rest. Therefore it’s the combination of dominance in sports and
        exceptional athletes that propel the U.S. to the top.
        <br /> <br /> <br />
        But how long can the U.S. enjoy this success? Nothing lasts forever, as the
        composition of sports is always evolving and athletes emerge and retire.
        Since exceptionality in both sports and athletes is necessary for success,
        it’s important to identify the next generation of sports and athletes to
        focus on and invest in in order to continue the United States's Olympic glory.
        <br />
        ↓
      </p>
    </section>

    <section class="rising-sports">
      <h3>Team USA Rising Sports</h3>
      <p class="instructions">
        Select the checkbox to reveal the performance trends for sports that
        haven't been in the top 5 for Team USA (yet...)
      </p>
      <br />
      <p class="instructions">
        Then scroll to the next section to reveal the 5 sports, and the
        corresponding athletes, that show the most potential and make the best
        candidates for the U.S. to focus on and invest in in the future.
      </p>
      <label for="show" style="display: inline;">Show Line:</label>
      <input id="show" type="checkbox" bind:checked={show} />

      <div class="row">
        <Rising data={archery} {show} title="Archery" />
        <Rising data={badminton} {show} title="Badminton" />
        <Rising data={boxing} {show} title="Boxing" />
        <Rising data={canoecayak} {show} title="Canoecayak" />
        <Rising data={cycling} {show} title="Cycling" />
        <Rising data={fencing} {show} title="Fencing" />
      </div>
      <div class="row">
        <Rising data={handball} {show} title="Handball" />
        <Rising data={hockey} {show} title="Hockey" />
        <Rising data={judo} {show} title="Judo" />
        <Rising data={pentathlon} {show} title="Pentathlon" />
        <Rising data={shooting} {show} title="Shooting" />
        <Rising data={softball} {show} title="Softball" />
      </div>
      <div class="row">
        <Rising data={tabletennis} {show} title="TableTennis" />
        <Rising data={taekwondo} {show} title="Taekwondo" />
        <Rising data={tennis} {show} title="Tennis" />
        <Rising data={triathlon} {show} title="Triathlon" />
        <Rising data={weightlifting} {show} title="Weightlifting" />
        <Rising data={wrestling} {show} title="Wrestling" />
      </div>
    </section>

    <section class="top-sports-rising">
      Top 5 Rising Sports and Athletes<br />
      <Top5 />
    </section>

    <section class="conclusion">
      <h1 class="title">Closing Remarks</h1>
      <h2 class="intro">
        The United States is consistently the top performing country in the
        Olympics. What fuels their success though isn’t external factors such as
        home advantage. Rather, their dominance in the Olympics can be
        attributed to excelling in certain sports like <span class="highlight"
          >aquatics</span
        >
        and <span class="highlight">athletics</span>, and to superstar athletes
        that consistently help drive significant success in these sports. Thus,
        it’s the combination of exceptional performance in certain sports and
        exceptional athletes that pushes the U.S. above the others. However,
        change is inevitable. Sports have evolved greatly over the last hundreds
        of years, and the changing nature of society is bound to affect the
        composition of sports. Similarly, athletes are constantly developing and
        retiring. Since shifting landscapes and emerging talents are bound to
        reshape the narrative of the United States in the Olympics, it’s
        important to discover areas for future investment and growth. In
        particular, <span class="highlight">boxing</span>,
        <span class="highlight">fencing</span>,
        <span class="highlight">handball</span>,
        <span class="highlight">pentathlon</span>,
        <span class="highlight">shooting</span> and their respective rising athletes,
        show great potential in sustaining Olympic excellence.
      </h2>
    </section>
  </div>
</Scroller>

<style>
  .box {
    display: flex;
  }

  .box .inner {
    width: 800px;
    height: 200px;
    line-height: 200px;
    font-size: 4em;
    font-family: sans-serif;
    font-weight: bold;
    white-space: nowrap;
    overflow: hidden;
  }

  .box .inner:first-child {
    background-color: lightskyblue;
    color: rgb(53, 127, 206);
    transform-origin: right;
    transform: perspective(100px) rotateY(-15deg);
  }

  .box .inner:last-child {
    background-color: lightskyblue;
    color: rgb(53, 127, 206);
    transform-origin: left;
    transform: perspective(100px) rotateY(15deg);
  }

  .box .inner span {
    position: absolute;
    animation: marquee 5s linear infinite;
  }

  .box .inner:first-child span {
    animation-delay: 2.5s;
    left: -100%;
  }

  @keyframes marquee {
    from {
      left: 100%;
    }

    to {
      left: -100%;
    }
  }

  .olympic-logo {
    width: 120px;
    height: 1200px;
    background-image: url('logo.png');
    background-size: contain;
    background-repeat: no-repeat;
    position: relative;
    bottom: -20px;
    left: -100px;
    animation: moveLogo 10s linear infinite;
  }

  @keyframes moveLogo {
    from {
      left: -100px;
    }
    to {
      left: calc(100% + 100px);
    }
  }
  .background {
    width: 100%;
    height: 100vh;
    position: relative;
    font-family: 'Times New Roman';
  }

  h3 {
    margin-top: 10px;
  }
  .instructions {
    font-size: 16px;
    margin-top: -20px;
    font-style: italic;
    font-family: arial;
    margin-left: 3px;
    margin-right: 3px;
  }
  .explanation1 {
    font-size: 18px;
    font-family: 'times new roman';
    margin-top: 0px;
    display: flex;
  }
  .explanation2 {
    font-size: 18px;
    font-family: 'times new roman';
    margin-top: -250px;
    margin-left: 3px;
    margin-right: 3px;
    display: flex;
  }
  .explanation3 {
    font-size: 18px;
    font-family: 'times new roman';
    margin-top: 490px;
    display: flex;
    overflow-y: auto;
  }
  .explanation4 {
    font-size: 18px;
    font-family: 'times new roman';
    margin-top: 100px;
    display: flex;
  }
  .explanation5 {
    font-size: 22px;
    font-family: 'times new roman';
    margin-top: 200px;
    margin-left: 200px;
    margin-right: 200px;
    display: flex;
  }
  .title {
    font-family: 'Times New Roman';
    font-size: 100px;
    font-weight: bold;
    color: white;
    text-shadow:
      0px 0px 5px #30dce5,
      0px 0px 10px #30dce5,
      0px 0px 10px #30dce5,
      0px 0px 20px #b393d3;
  }
  .intro {
    font-size: 25px;
    margin-left: 40px;
    margin-right: 40px;
  }
  .highlight {
    color: #1d74d7;
  }
  .foreground {
    width: 100%;
    margin: 0 auto;
    height: auto;
    position: relative;
  }

  section {
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.1);
    color: white;
    text-align: center;
    max-width: 100%;
    color: black;
    font-family: 'times new roman';
    text-align: center;
    font-size: 35px;
    line-height: 28px;
    font-weight: bold;
    padding-top: 20px;
  }
  .intro-page {
    font-size: 20px;
    background-image: url('/b.jpeg');
    background-size: cover;
    background-position: center;
  }
  .proj3 {
    background-image: linear-gradient(
      to bottom right,
      rgba(0, 255, 0, 0.5),
      rgba(0, 100, 0, 0.5)
    );
  }

  .home-advantage-2 {
    background-image: linear-gradient(
      to bottom right,
      rgba(255, 255, 0, 0.5),
      rgba(255, 0, 0, 0.5)
    );
  }

  .top-sports {
    background-image: linear-gradient(
      to bottom right,
      rgba(0, 0, 255, 0.5),
      rgba(0, 255, 255, 0.5)
    );
  }
  .home-advantage-1 {
    background-image: linear-gradient(
      to bottom right,
      rgba(128, 0, 128, 0.5),
      rgba(255, 192, 203, 0.5)
    );
  }
  .top-athletes {
    background-image: linear-gradient(
      to bottom right,
      rgba(0, 0, 128, 0.5),
      rgba(0, 0, 0, 0.5)
    );
  }
  .transition-section {
    background-image: linear-gradient(
      to bottom right,
      rgba(127, 3, 104, 0.5),
      rgba(15, 201, 230, 0.5)
    );
  }
  .rising-sports {
    width: 100%;
    overflow: auto;
    padding: 10px;
    background-image: linear-gradient(
      to bottom right,
      rgba(6, 118, 92, 0.5),
      rgba(28, 218, 91, 0.5)
    );
  }
  .top-sports-rising {
    background-image: linear-gradient(
      to bottom right,
      rgba(4, 17, 199, 0.5),
      rgba(84, 142, 229, 0.5)
    );
  }

  .top-countries {
    background-image: linear-gradient(
      to bottom right,
      rgba(0, 0, 128, 0.5),
      rgba(0, 0, 0, 0.5)
    );
  }

  .row {
    font-size: 15px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-bottom: -10px;
    margin-top: 30px;
    margin-left: 100px;
    margin-right: -250px;
  }

  .conclusion {
    background-image: url('/b.jpeg');
    background-size: cover;
    background-position: center;
  }
</style>
