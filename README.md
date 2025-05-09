<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Sorteio de Times da Pelada</title>
  <style>
    body {
      font-family: sans-serif;
      background: #f4f4f4;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    button {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      font-size: 18px;
    }
    .team {
      background: white;
      border-radius: 8px;
      padding: 10px;
      margin: 10px 0;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    .team h3 {
      margin: 0 0 5px 0;
    }
  </style>
</head>
<body>

  <h1>Sorteador de Times - Pelada</h1>
  <button onclick="sortearTimes()">Sortear Times</button>

  <div id="resultado"></div>

  <script>
    const jogadores = [
      { nome: "Arthur", estrelas: 1 },
      { nome: "Luca", estrelas: 3 },
      { nome: "João", estrelas: 3 },
      { nome: "Rafa", estrelas: 5 },
      { nome: "Lucas", estrelas: 3 },
      { nome: "JP", estrelas: 5 },
      { nome: "Pedro", estrelas: 5 },
      { nome: "DG", estrelas: 3 },
      { nome: "Wilson", estrelas: 1 },
      { nome: "Kayan", estrelas: 5 },
      { nome: "Marcelo", estrelas: 1 },
      { nome: "Virgem", estrelas: 3 },
      { nome: "Perfeito", estrelas: 1 }
    ];

    function embaralhar(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
    }

    function sortearTimes() {
      const copia = [...jogadores];
      embaralhar(copia);

      const resultadoDiv = document.getElementById("resultado");
      resultadoDiv.innerHTML = "";

      const numTimes = Math.floor(copia.length / 4);
      for (let i = 0; i < numTimes; i++) {
        const time = copia.slice(i * 4, (i + 1) * 4);
        const estrelasTotal = time.reduce((soma, j) => soma + j.estrelas, 0);
        const timeDiv = document.createElement("div");
        timeDiv.className = "team";
        timeDiv.innerHTML = `
          <h3>Time ${i + 1} - ${estrelasTotal} ⭐</h3>
          <ul>
            ${time.map(j => `<li>${j.nome} (${j.estrelas}⭐)</li>`).join("")}
          </ul>
        `;
        resultadoDiv.appendChild(timeDiv);
      }

      // Se sobrar jogadores
      const sobra = copia.slice(numTimes * 4);
      if (sobra.length > 0) {
        const sobraDiv = document.createElement("div");
        sobraDiv.className = "team";
        sobraDiv.innerHTML = `
          <h3>Jogadores sobrando</h3>
          <ul>
            ${sobra.map(j => `<li>${j.nome} (${j.estrelas}⭐)</li>`).join("")}
          </ul>
        `;
        resultadoDiv.appendChild(sobraDiv);
      }
    }
  </script>

</body>
</html>
