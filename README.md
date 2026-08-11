[index.html](https://github.com/user-attachments/files/30941071/index.html)
# mot_fleche_esg
Mot Fleché ESG 2026
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Le mot fléché de la rentrée | ekodev by EPSA</title>
<meta name="description" content="Un petit jeu RSE avant la rentrée : quatre mots se cachent dans l'actualité de l'été 2026, par ekodev by EPSA.">
<style>
  :root{
    --forest: #0B3B3C;
    --forest-deep: #072526;
    --gold: #F2C230;
    --gold-ink: #6b4f06;
    --blue-grey: #9FB6BE;
    --paper: #FFFFFF;
    --paper-soft: #F5F7F6;
    --ink: #12201F;
    --ink-soft: #4C5A58;
    --line: #DDE4E2;
    --radius: 10px;
  }

  *{ box-sizing: border-box; }

  html{ -webkit-text-size-adjust: 100%; }

  body{
    margin: 0;
    background: var(--paper-soft);
    color: var(--ink);
    font-family: -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif;
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
  }

  a{ color: var(--forest); }
  a:focus-visible,
  button:focus-visible,
  input:focus-visible{
    outline: 3px solid var(--gold);
    outline-offset: 2px;
  }

  /* ---------- Header ---------- */
  header{
    background: var(--forest);
    color: #fff;
    padding: 2.25rem 1.25rem 2.5rem;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  header::before{
    /* clin d'oeil discret au motif circulaire de la marque, sans dégradé criard */
    content: "";
    position: absolute;
    top: -60px;
    left: -60px;
    width: 180px;
    height: 180px;
    border: 22px solid rgba(242, 194, 48, 0.16);
    border-radius: 50%;
  }
  .brand{
    display: inline-flex;
    align-items: baseline;
    gap: .35rem;
    font-size: .95rem;
    letter-spacing: .02em;
    color: var(--blue-grey);
    margin-bottom: 1.1rem;
  }
  .brand strong{
    color: #fff;
    font-weight: 700;
    font-size: 1.05rem;
  }
  header h1{
    margin: 0 auto;
    max-width: 30rem;
    font-size: clamp(1.5rem, 4.5vw, 2.1rem);
    font-weight: 800;
    letter-spacing: -0.01em;
    position: relative;
  }
  header p.kicker{
    margin: .6rem auto 0;
    max-width: 26rem;
    color: rgba(255,255,255,0.78);
    font-size: .95rem;
    position: relative;
  }

  /* ---------- Main ---------- */
  main{
    max-width: 640px;
    margin: 0 auto;
    padding: 2rem 1.25rem 3rem;
  }

  .intro{
    text-align: center;
    color: var(--ink-soft);
    font-size: 1rem;
    margin: 0 0 2rem;
  }
  .intro strong{ color: var(--ink); }

  /* ---------- Fallback (no-JS) ---------- */
  .fallback{
    background: var(--paper);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 1.25rem 1.25rem 1.5rem;
    margin-bottom: 2rem;
  }
  .fallback h2{
    font-size: 1rem;
    margin: 0 0 .75rem;
  }
  .fallback ol{ margin: 0; padding-left: 1.2rem; }
  .fallback li{ margin-bottom: .5rem; }
  .fallback details{ margin-top: 1rem; }
  .fallback summary{
    cursor: pointer;
    font-weight: 700;
    color: var(--forest);
  }
  .fallback .answers{ margin-top: .6rem; color: var(--ink-soft); }

  /* ---------- Puzzle ---------- */
  #puzzle{
    display: flex;
    flex-direction: column;
    gap: 1.4rem;
  }

  .clue-card{
    background: var(--paper);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 1rem 1.1rem 1.15rem;
    transition: border-color .15s ease;
  }
  .clue-card.is-complete{
    border-color: var(--gold);
  }

  .clue-head{
    display: flex;
    align-items: flex-start;
    gap: .65rem;
    margin-bottom: .85rem;
  }
  .clue-number{
    flex: none;
    width: 1.6rem;
    height: 1.6rem;
    border-radius: 50%;
    background: var(--forest);
    color: #fff;
    font-size: .8rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .clue-text{
    font-size: .92rem;
    color: var(--ink);
  }

  .cells-row{
    display: flex;
    align-items: center;
    gap: .5rem;
    padding-left: 2.25rem;
  }
  .arrow{
    flex: none;
    width: 18px;
    height: 18px;
    color: var(--gold-ink);
  }
  .cells{
    display: flex;
    gap: .3rem;
    flex-wrap: nowrap;
    overflow-x: auto;
    padding-bottom: 2px;
  }
  .cells input{
    flex: none;
    width: 2.05rem;
    height: 2.35rem;
    text-align: center;
    text-transform: uppercase;
    font-size: 1.05rem;
    font-weight: 700;
    font-family: inherit;
    color: var(--ink);
    background: var(--paper-soft);
    border: 1.5px solid var(--line);
    border-radius: 6px;
    caret-color: var(--forest);
  }
  .cells input:focus{
    background: #fff;
    border-color: var(--forest);
  }
  .cells input.is-revealed{
    background: #FCF3D8;
    border-color: var(--gold);
    color: var(--gold-ink);
  }

  /* ---------- Actions ---------- */
  .actions{
    margin-top: 1.75rem;
    text-align: center;
  }
  #reveal-btn{
    appearance: none;
    border: none;
    background: var(--gold);
    color: var(--forest-deep);
    font-family: inherit;
    font-weight: 700;
    font-size: .95rem;
    padding: .8rem 1.6rem;
    border-radius: 999px;
    cursor: pointer;
  }
  #reveal-btn:hover{ background: #e6b41c; }
  .actions p{
    margin: .75rem 0 0;
    font-size: .82rem;
    color: var(--ink-soft);
  }

  /* ---------- Footer ---------- */
  footer{
    text-align: center;
    padding: 1.5rem 1.25rem 2.5rem;
    color: var(--ink-soft);
    font-size: .85rem;
    border-top: 1px solid var(--line);
  }
  footer a{
    color: var(--ink-soft);
    text-decoration: none;
    font-weight: 600;
  }
  footer a:hover{ color: var(--forest); }

  @media (min-width: 480px){
    .cells input{ width: 2.3rem; height: 2.5rem; font-size: 1.15rem; }
  }

  @media (prefers-reduced-motion: reduce){
    .clue-card{ transition: none; }
  }
</style>
</head>
<body>

<header>
  <div class="brand"><strong>ekodev</strong> by epsa</div>
  <h1>🧩 Le mot fléché de la rentrée</h1>
  <p class="kicker">Un dernier jeu avant de reprendre les choses sérieuses.</p>
</header>

<main>
  <p class="intro">
    Cet été a été (vraiment) chaud. <strong>Quatre mots</strong> s'y cachent —
    trouvez-les, ils annoncent tout ce qui vous attend à la rentrée.
  </p>

  <!-- Contenu accessible sans JavaScript -->
  <noscript>
    <div class="fallback">
      <h2>Les indices</h2>
      <ol id="noscript-clues"></ol>
      <details>
        <summary>Voir les réponses</summary>
        <p class="answers" id="noscript-answers"></p>
      </details>
    </div>
  </noscript>

  <div id="puzzle" aria-live="polite"></div>

  <div class="actions">
    <button id="reveal-btn" type="button">Voir les réponses</button>
    <p>Ça ne réinitialise rien de ce que vous avez déjà tapé 🙂</p>
  </div>
</main>

<footer>
  <a href="https://www.ekodev.com" target="_blank" rel="noopener">ekodev.com →</a>
</footer>

<script>
(function () {
  "use strict";

  /* ------------------------------------------------------------
     Contenu du mot fléché — à mettre à jour chaque année.
     Chaque entrée : { indice: texte de la définition, reponse: mot en MAJUSCULES sans accent ni espace }
  ------------------------------------------------------------ */
  var MOTS = [
    {
      indice: "On l'a vécue trois fois depuis mai, la dernière ayant battu tous les records de juillet.",
      reponse: "CANICULE"
    },
    {
      indice: "Le mot que la France — et votre organisation — vont devoir conjuguer avec le climat, encore et encore.",
      reponse: "ADAPTATION"
    },
    {
      indice: "Le nouveau standard européen qui évite à votre PME/ETI de crouler sous les questionnaires ESG de vos clients.",
      reponse: "VSME"
    },
    {
      indice: "Le maillon de votre chaîne de valeur qui concentre l'essentiel de votre empreinte carbone (indice : ce n'est pas votre siège).",
      reponse: "ACHATS"
    }
  ];

  var puzzleEl = document.getElementById("puzzle");
  var revealBtn = document.getElementById("reveal-btn");
  var noscriptClues = document.getElementById("noscript-clues");
  var noscriptAnswers = document.getElementById("noscript-answers");

  var ARROW_SVG =
    '<svg class="arrow" viewBox="0 0 24 24" fill="none" aria-hidden="true">' +
    '<path d="M4 12h14M13 6l6 6-6 6" stroke="currentColor" stroke-width="2.4" ' +
    'stroke-linecap="round" stroke-linejoin="round"/></svg>';

  function buildNoscriptFallback() {
    // Rempli même si JS tourne, au cas où (ne coûte rien) ; masqué par <noscript> côté rendu.
    MOTS.forEach(function (mot) {
      var li = document.createElement("li");
      li.textContent = mot.indice + " (" + mot.reponse.length + " lettres)";
      noscriptClues.appendChild(li);
    });
    noscriptAnswers.textContent = MOTS.map(function (m) { return m.reponse; }).join(" · ");
  }

  function buildPuzzle() {
    MOTS.forEach(function (mot, wordIndex) {
      var card = document.createElement("section");
      card.className = "clue-card";
      card.setAttribute("data-word-index", wordIndex);

      var head = document.createElement("div");
      head.className = "clue-head";

      var number = document.createElement("span");
      number.className = "clue-number";
      number.textContent = wordIndex + 1;
      number.setAttribute("aria-hidden", "true");

      var clueId = "clue-" + wordIndex;
      var text = document.createElement("p");
      text.className = "clue-text";
      text.id = clueId;
      text.textContent = mot.indice;

      head.appendChild(number);
      head.appendChild(text);

      var row = document.createElement("div");
      row.className = "cells-row";
      row.innerHTML = ARROW_SVG;

      var cells = document.createElement("div");
      cells.className = "cells";
      cells.setAttribute("role", "group");
      cells.setAttribute("aria-labelledby", clueId);

      for (var i = 0; i < mot.reponse.length; i++) {
        var input = document.createElement("input");
        input.type = "text";
        input.maxLength = 1;
        input.autocomplete = "off";
        input.autocapitalize = "characters";
        input.spellcheck = false;
        input.inputMode = "text";
        input.setAttribute("aria-label", "Lettre " + (i + 1) + " sur " + mot.reponse.length);
        input.setAttribute("data-word-index", wordIndex);
        input.setAttribute("data-letter-index", i);
        cells.appendChild(input);
      }

      row.appendChild(cells);
      card.appendChild(head);
      card.appendChild(row);
      puzzleEl.appendChild(card);
    });
  }

  function allInputsForWord(wordIndex) {
    return Array.prototype.slice.call(
      puzzleEl.querySelectorAll('input[data-word-index="' + wordIndex + '"]')
    );
  }

  function checkWordComplete(wordIndex) {
    var inputs = allInputsForWord(wordIndex);
    var value = inputs.map(function (inp) { return inp.value.toUpperCase(); }).join("");
    var card = puzzleEl.querySelector('.clue-card[data-word-index="' + wordIndex + '"]');
    if (value === MOTS[wordIndex].reponse) {
      card.classList.add("is-complete");
    } else {
      card.classList.remove("is-complete");
    }
  }

  function handleInput(e) {
    var target = e.target;
    if (target.tagName !== "INPUT") return;

    var value = target.value.replace(/[^a-zA-ZÀ-ÿ]/g, "").toUpperCase();
    target.value = value.slice(-1);
    target.classList.remove("is-revealed");

    var wordIndex = target.getAttribute("data-word-index");
    var letterIndex = parseInt(target.getAttribute("data-letter-index"), 10);

    if (target.value) {
      var inputs = allInputsForWord(wordIndex);
      var next = inputs[letterIndex + 1];
      if (next) next.focus();
    }

    checkWordComplete(wordIndex);
  }

  function handleKeydown(e) {
    var target = e.target;
    if (target.tagName !== "INPUT") return;

    var wordIndex = target.getAttribute("data-word-index");
    var letterIndex = parseInt(target.getAttribute("data-letter-index"), 10);
    var inputs = allInputsForWord(wordIndex);

    if (e.key === "Backspace" && !target.value && letterIndex > 0) {
      var prev = inputs[letterIndex - 1];
      if (prev) {
        prev.focus();
        prev.value = "";
        checkWordComplete(wordIndex);
      }
    } else if (e.key === "ArrowLeft" && letterIndex > 0) {
      e.preventDefault();
      inputs[letterIndex - 1].focus();
    } else if (e.key === "ArrowRight" && letterIndex < inputs.length - 1) {
      e.preventDefault();
      inputs[letterIndex + 1].focus();
    }
  }

  function revealAnswers() {
    MOTS.forEach(function (mot, wordIndex) {
      var inputs = allInputsForWord(wordIndex);
      inputs.forEach(function (input, letterIndex) {
        var correctLetter = mot.reponse[letterIndex];
        if (input.value.toUpperCase() !== correctLetter) {
          input.value = correctLetter;
          input.classList.add("is-revealed");
        }
      });
      checkWordComplete(wordIndex);
    });
  }

  buildNoscriptFallback();
  buildPuzzle();

  puzzleEl.addEventListener("input", handleInput);
  puzzleEl.addEventListener("keydown", handleKeydown);
  revealBtn.addEventListener("click", revealAnswers);
})();
</script>

</body>
</html>
