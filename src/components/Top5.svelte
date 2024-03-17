<script>
  let boxing = false;
  let fencing = false;
  let handball = false;
  let pentathlon = false;
  let shooting = false;

  const handleMouseenter = () => (
    (boxing = true),
    (fencing = true),
    (handball = true),
    (pentathlon = true),
    (shooting = true)
  );
  const handleMouseleave = () => (
    (boxing = false),
    (fencing = false),
    (handball = false),
    (pentathlon = false),
    (shooting = false)
  );
</script>

<div
  style="display: flex; flex-wrap: wrap; justify-content: center; margin-bottom: -60px"
>
  <div
    style="margin-right: 10px; text-align:center;"
    on:mouseenter={() => handleMouseenter('boxing')}
    on:mouseleave={handleMouseleave}
  >
    <a href="https://www.olympedia.org/athletes/113051" target="_blank">
      <img
        class:curious={boxing}
        alt="boxing"
        src="boxing.png"
        style="width: 20vw; height: auto;"
      />

      <p style="visibility: {boxing ? 'visible' : 'hidden'};">
        Boxing: Deontay Wilder
      </p>
    </a>
  </div>
  <div
    style="margin-right: 10px; text-align:center;"
    on:mouseenter={() => handleMouseenter('fencing')}
    on:mouseleave={handleMouseleave}
  >
    <a
      href="https://www.usafencing.org/page/show/700900-mariel-zagunis"
      target="_blank"
    >
      <img
        class:curious={fencing}
        alt="fencing"
        src="fencing.png"
        style="width:25vw; height: auto;"
      />

      <p style="visibility: {fencing ? 'visible' : 'hidden'};">
        Fencing: Mariel Zagunis
      </p>
    </a>
  </div>
  <div
    style="margin-right: 10px; text-align:center;"
    on:mouseenter={() => handleMouseenter('handball')}
    on:mouseleave={handleMouseleave}
  >
    <a
      href="https://www.usateamhandball.org/profiles/gary-hines"
      target="_blank"
    >
      <img
        class:curious={handball}
        alt="handball"
        src="handball.png"
        style="width: 20vw; height: auto;"
      />
      <p style="visibility: {handball ? 'visible' : 'hidden'};">
        Handball: Gary Hines
      </p>
    </a>
  </div>
</div>
<div style="display: flex; flex-wrap: wrap; justify-content: center;">
  <div
    style="margin-right: 10px; text-align:center;"
    on:mouseenter={() => handleMouseenter('pentathlon')}
    on:mouseleave={handleMouseleave}
  >
    <a href="https://www.teamusa.com/profiles/sheila-taormina" target="_blank">
      <img
        class:curious={pentathlon}
        alt="pentathlon"
        src="pentathlon.png"
        style="width: 20vw; height: auto;"
      />
      <p style="visibility: {pentathlon ? 'visible' : 'hidden'};">
        Pentathlon: Sheila Taormina
      </p>
    </a>
  </div>
  <div
    style="margin-right: 10px; text-align:center;"
    on:mouseenter={() => handleMouseenter('shooting')}
    on:mouseleave={handleMouseleave}
  >
    <a
      href="https://www.teamusa.com/profiles/vincent-hancock-848530"
      target="_blank"
    >
      <img
        class:curious={shooting}
        alt="shooting"
        src="shooting.png"
        style="width: 20vw; height: auto;"
      />
      <p style="visibility: {shooting ? 'visible' : 'hidden'};">
        Shooting: Vincent Hancock
      </p>
    </a>
  </div>
</div>

<style>
  img {
    position: relative;
    bottom: -60px;
    transform: translate(-400%, 0) rotate(-40deg);
    transform-origin: 100% 100%;
    transition: transform 0.4s;
    margin-left: 10px;
    margin-right: 10px;
  }

  .curious {
    transform: translate(0%, 0) rotate(0deg);
  }
  p {
    margin-top: 75px;
    font-family: sans-serif;
    font-size: 20px;
    display: flex;
  }
</style>
