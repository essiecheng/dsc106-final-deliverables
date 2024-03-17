<script>
  import { onDestroy } from 'svelte';
  import { tweened } from 'svelte/motion';
  import * as easingFns from 'svelte/easing';
  import Events from './Events.svelte';
  import { phelpsEvent } from './phelps.js';
  import { fischerEvent } from './fischer.js';
  import { thompsonEvent } from './thompson.js';

  // button
  let showButton = true;
  let showTop3 = false;
  let showTop2 = false;
  let showTop1 = false;

  function revealTop3() {
    showButton = false;
    showTop3 = true;
    showTop2 = false;
    showTop1 = false;
  }

  function revealTop2() {
    showButton = false;
    showTop3 = false;
    showTop2 = true;
    showTop1 = false;
  }

  function revealTop1() {
    showButton = false;
    showTop3 = false;
    showTop2 = false;
    showTop1 = true;
  }

  let showInfo = false;
  let info = '';
  let currentMode = 'medal';

  const names = Object.keys(easingFns).filter(
    (n) => !['default', '__moduleExports'].includes(n)
  );
</script>

{#if showInfo}
  <div class="medal-info">
    {info}
  </div>
{/if}

{#if showButton}
  <button on:click={revealTop1} class="big-button">1st Place</button>
  <button on:click={revealTop2} class="big-button">2nd Place</button>
  <button on:click={revealTop3} class="big-button">3rd Place</button>
{/if}

{#if showTop3}
  <div class="container-thompson">
    <button on:click={revealTop1} class="big-button">1st Place</button>
    <button on:click={revealTop2} class="big-button">2nd Place</button>
    <button on:click={revealTop3} class="big-button">3rd Place</button>
    <div class="thompson-info">
      <h4>Jenny Thompson</h4>
      <h2><u>Career Highlights</u></h2>
      <ul>
        <li>
          Competed in four consecutive Olympic Games, earning a total of 12
          medals, including eight golds.
        </li>
        <li>Named the World Swimmer of the Year in 1998.</li>
        <li>
          Competed collegiately at Stanford, earning 19 NCAA individual and
          relay titles.
        </li>
        <li>Set 6 World Records in long course meters</li>
      </ul>
    </div>
    <div class="timeline">
      {#each thompsonEvent as { Year, City, Event, Medal }}
        <Events year={Year} city={City} event={Event} medal={Medal} />
      {/each}
    </div>
  </div>
{/if}

{#if showTop2}
  <div class="container-fischer">
    <button on:click={revealTop1} class="big-button">1st Place</button>
    <button on:click={revealTop2} class="big-button">2nd Place</button>
    <button on:click={revealTop3} class="big-button">3rd Place</button>
    <h4>Birgit Fischer</h4>
    <h2><u>Career Highlights</u></h2>
    <ul>
      <li>
        Most Olympic Medals among Olympic kayakers: 12 Olympic medals (6 gold, 4
        silver, 2 bronze)
      </li>
      <li>Only Woman to win Olympic medals 20 years apart.</li>
      <li>
        Most Consecutive World Championship Wins: Fischer won three consecutive
        World Championships from 1981 to 1983.
      </li>
    </ul>
    <div class="timeline">
      {#each fischerEvent as { Year, City, Event, Medal }}
        <Events year={Year} city={City} event={Event} medal={Medal} />
      {/each}
    </div>
  </div>
{/if}

{#if showTop1}
  <div class="container-phelps">
    <button on:click={revealTop1} class="big-button">1st Place</button>
    <button on:click={revealTop2} class="big-button">2nd Place</button>
    <button on:click={revealTop3} class="big-button">3rd Place</button>
    <h4>Michael Phelps</h4>
    <h2><u>Career Highlights</u></h2>
    <ul>
      <li>Most gold medals overall in World Championship history.</li>
      <li>
        Most gold medals won at a single Olympics: 8 gold medals in 2008 Beijing
        Olympics.
      </li>
      <li>Most Olympic medals of any athlete: 16 total medals.</li>
      <li>Currently holds the most world records in swimming with 7</li>
    </ul>
    <div class="timeline">
      {#each phelpsEvent as { Year, City, Event, Medal }}
        <Events year={Year} city={City} event={Event} medal={Medal} />
      {/each}
    </div>
  </div>
{/if}

<style>
  .big-button {
    padding: 0.6em 2em;
    border: none;
    outline: none;
    color: rgb(255, 255, 255);
    background: #111;
    cursor: pointer;
    position: relative;
    z-index: 0;
    border-radius: 10px;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
  }
  .big-button:before {
    content: '';
    background: linear-gradient(
      45deg,
      #ff0000,
      #ff7300,
      #fffb00,
      #48ff00,
      #00ffd5,
      #002bff,
      #7a00ff,
      #ff00c8,
      #ff0000
    );
    position: absolute;
    top: -2px;
    left: -2px;
    background-size: 400%;
    z-index: -1;
    filter: blur(5px);
    -webkit-filter: blur(5px);
    width: calc(100% + 4px);
    height: calc(100% + 4px);
    animation: glowing-big-button 20s linear infinite;
    transition: opacity 0.3s ease-in-out;
    border-radius: 10px;
  }
  @keyframes glowing-big-button {
    0% {
      background-position: 0 0;
    }
    50% {
      background-position: 400% 0;
    }
    100% {
      background-position: 0 0;
    }
  }
  .big-button:after {
    z-index: -1;
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    background: #222;
    left: 0;
    top: 0;
    border-radius: 10px;
  }

  .container-fischer {
    text-align: center;
    width: 100%;
    height: 100vh;
    max-height: 100vh;
    position: relative;
    background-image: url('fischer.png');
    background-size: 48%;
    background-repeat: no-repeat;
    background-position: 0% 30%;
    background-color: linear-gradient(
      to bottom right,
      rgba(0, 0, 128, 0.5),
      rgba(0, 0, 0, 0.5)
    );
  }

  .container-thompson {
    text-align: center;
    width: 100%;
    height: 100vh;
    max-height: 100vh;
    position: relative;
    background-image: url('thompson.png');
    background-size: 30%;
    background-repeat: no-repeat;
    background-position: 5% 5%;
    background-color: linear-gradient(
      to bottom right,
      rgba(0, 0, 128, 0.5),
      rgba(0, 0, 0, 0.5)
    );
  }

  .container-phelps {
    text-align: center;
    width: 100%;
    height: 100vh;
    max-height: 100vh;
    overflow: hidden;
    position: relative;
    background-image: url('phelps.png');
    background-size: 60%;
    background-repeat: no-repeat;
    background-position: -35% 0%;
    background-color: linear-gradient(
      to bottom right,
      rgba(0, 0, 128, 0.5),
      rgba(0, 0, 0, 0.5)
    );
  }

  .timeline {
    position: absolute;
    top: 0;
    right: 0;
    width: 450px;
    height: 86.5%;
    background-color: linear-gradient(
      to bottom right,
      rgba(0, 0, 128, 0.5),
      rgba(0, 0, 0, 0.5)
    );
    font-family: Helvetica, sans-serif;
    overflow-x: hidden;
    overflow-y: auto;
    font-size: 14px;
    font-family: times new roman;
  }

  @media screen and (max-width: 600px) {
    .timeline::after {
      left: 31px;
    }
  }

  h2 {
    font-size: 25px;
    margin-top: -30px;
  }

  h4 {
    font-size: 45px;
    font-weight: 500, 'bold';
    text-transform: uppercase;
    line-height: 1;
    text-align: center;
    font-family: 'times new roman';
    color: white;
    margin-top: 40px;
  }

  ul {
    padding: 0;
    margin: 0 auto;
    text-align: center;
    width: 35%;
    font-size: 18px;
    list-style: none;
    margin-right: 30%;
  }

  * {
    box-sizing: border-box;
  }

  li + li {
    margin-top: 0.5rem;
  }

  li {
    display: flex;
    align-items: center;
    gap: 1rem;
    background: aliceblue;
    padding: 1rem;
    border-radius: 1rem;
    width: calc(100% - 5rem);
    box-shadow: 0.25rem 0.25rem 0.75rem rgb(0 0 0 / 0.1);
  }

  li:nth-child(even) {
    flex-direction: row-reverse;
    background: honeydew;
  }

  li:nth-child(even)::before {
    transform: rotateY(180deg);
  }
</style>
