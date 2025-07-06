<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<title>Peça Romântica Personalizada</title>
<style>
  body {
    margin: 0;
    background: linear-gradient(135deg, #fceabb, #f8b500);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: #5a2a27;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    overflow: hidden;
  }
  h1 {
    margin-top: 30px;
    font-size: 2.8rem;
    font-weight: 900;
    text-shadow: 2px 2px 6px #a25244;
  }
  #palco {
    position: relative;
    background: #fff0f5;
    width: 600px;
    height: 360px;
    border-radius: 25px;
    box-shadow: 0 0 25px #f48fb1;
    margin-top: 30px;
    padding: 20px;
    box-sizing: border-box;
  }
  .personagem {
    position: absolute;
    bottom: 20px;
    width: 140px;
    height: 210px;
    background: #f48fb1;
    border-radius: 20px;
    box-shadow: 0 0 15px #f06292;
    color: white;
    font-weight: 700;
    text-align: center;
    padding-top: 180px;
    font-size: 1.2rem;
    user-select: none;
    opacity: 0.4;
    transition: opacity 0.5s ease, transform 0.5s ease;
    background-size: cover;
    background-position: center;
  }
  .personagem.ativo {
    opacity: 1;
    box-shadow: 0 0 35px #f50057;
    transform: scale(1.05);
  }
  #eu {
    left: 30px;
    background-image: url('https://i.imgur.com/3qf6G0K.jpg'); /* sua foto */
  }
  #ela {
    right: 30px;
    background-image: url('https://i.imgur.com/8kQh6mj.jpg'); /* foto da sua namorada */
  }
  #balao {
    position: absolute;
    top: 40px;
    left: 50%;
    transform: translateX(-50%);
    max-width: 480px;
    background: #fff0f5;
    color: #ad1457;
    font-weight: 600;
    font-size: 20px;
    padding: 18px 28px;
    border-radius: 35px 35px 35px 5px;
    box-shadow: 3px 3px 15px rgba(245, 0, 87, 0.5);
    opacity: 0;
    transition: opacity 0.6s ease;
    text-align: center;
  }
  #balao.ativo {
    opacity: 1;
  }
  button {
    margin-top: 25px;
    padding: 14px 35px;
    font-size: 18px;
    font-weight: 700;
    border: none;
    border-radius: 35px;
    background: linear-gradient(135deg, #f50057, #ad1457);
    color: white;
    cursor: pointer;
    box-shadow: 0 6px 15px rgba(245, 0, 87, 0.7);
    transition: background 0.3s ease;
  }
  button:hover {
    background: linear-gradient(135deg, #ad1457, #f50057);
  }
</style>
</head>
<body>
  <h1>Peça Romântica para Você</h1>
  <div id="palco">
    <div id="eu" class="personagem">Eu</div>
    <div id="ela" class="personagem">Você</div>
    <div id="balao"></div>
  </div>
  <button id="btn-proximo">Próximo</button>

  <audio id="musica" src="https://cdn.pixabay.com/download/audio/2022/02/18/audio_c2f94f7f1b.mp3?filename=soft-romantic-piano-music-11386.mp3" loop></audio>

  <script>
    const falas = [
      { personagem: 'eu', texto: 'Desde que te conheci, meu mundo ficou mais colorido.' },
      { personagem: 'ela', texto: 'Você é meu sonho que virou realidade.' },
      { personagem: 'eu', texto: 'Cada momento contigo é um presente precioso.' },
      { personagem: 'ela', texto: 'Nosso amor é minha força e alegria.' },
      { personagem: 'eu', texto: 'Prometo estar sempre ao seu lado, para o que der e vier.' },
      { personagem: 'ela', texto: 'Juntos somos invencíveis, minha razão de sorrir.' },
      { personagem: 'eu', texto: 'Te amo mais do que palavras podem expressar.' },
      { personagem: 'ela', texto: 'E eu amo você, hoje e para sempre.' }
    ];

    let indice = 0;
    const balao = document.getElementById('balao');
    const personagens = {
      eu: document.getElementById('eu'),
      ela: document.getElementById('ela')
    };
    const musica = document.getElementById('musica');

    function mostrarFala() {
      const fala = falas[indice];
      balao.textContent = fala.texto;
      balao.classList.add('ativo');

      Object.values(personagens).forEach(p => p.classList.remove('ativo'));
      personagens[fala.personagem].classList.add('ativo');

      indice++;
      if(indice >= falas.length) indice = 0;
    }

    document.getElementById('btn-proximo').addEventListener('click', () => {
      // toca música na primeira interação (para evitar bloqueios do navegador)
      if(musica.paused) musica.play();

      balao.classList.remove('ativo');
      setTimeout(mostrarFala, 300);
    });

    mostrarFala();
  </script>
</body>
</html>
