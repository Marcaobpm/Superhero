# Superhero Viewer
Este projeto é uma aplicação React simples que utiliza a Superhero API para exibir informações sobre heróis selecionados, incluindo suas imagens e estatísticas de poder.

# Funcionalidades
Consulta a API de super-heróis para buscar dados de heróis específicos.
Exibição das informações de heróis, incluindo:
Nome
Imagem
Estatísticas de poder (inteligência e força) representadas graficamente.

# Tecnologias Utilizadas
React: Biblioteca JavaScript para a criação de interfaces de usuário.
CSS Modules: Para estilização modular e escopo local dos estilos.
Superhero API: API pública para acesso a informações sobre heróis.

# Pré-requisitos
Antes de rodar o projeto, você precisará de:

Node.js (versão 14 ou superior).
Um gerenciador de pacotes como npm ou yarn.
# Instalação
1. clone esse repositorio
```git clone https://github.com/seu-usuario/superhero-viewer.git```
   ```cd superhero-viewer ```
2. Instale as dependências:
   ```npm install```
3. Configure a variável ACCESS_TOKEN no arquivo page.module.css com sua chave de acesso à Superhero API. Caso ainda não possua uma, obtenha no site oficial da API.
# Uso
1. Inicie o servidor de desenvolvimento:
```npm run dev```
2. Abra o navegador e acesse:
```http://localhost:3000```
3. Veja as informações dos heróis exibidas na tela.

Código:
``` "use client";
 
import { useEffect, useState } from "react";
import styles from "./page.module.css";

const ACCESS_TOKEN = "4995282617154105";
const BASE_URL = https://superheroapi.com/api.php/${ACCESS_TOKEN}/;

export default function Home() {
  const [heroes, setHeroes] = useState([]);

  const fetchHero = async (id) => {
    try {
      const response = await fetch(${BASE_URL}${id});
      const data = await response.json();
      return data;
    } catch (error) {
      console.error("Erro ao buscar herói:", error);
      return null;
    }
  };

  useEffect(() => {
    const heroIds = [200, 465]; // IDs dos heróis
    const fetchHeroes = async () => {
      const heroData = await Promise.all(heroIds.map((id) => fetchHero(id)));
      setHeroes(heroData.filter(Boolean));
    };

    fetchHeroes();
  }, []);

  return (
    <div className={styles.heroes}>
      {heroes.map((hero) => (
        <article key={hero.id} className={styles.card}>
          <img src={hero.image.url} alt={hero.name} className={styles.image} />
          <h1>{hero.name}</h1>
          <p>
            Intelligence:{" "}
            <span
              className={styles.bar}
              style={{
                width: ${hero.powerstats.intelligence}%,
                backgroundColor: "#F9B32F",
              }}
            />
          </p>
          <p>
            Strength:{" "}
            <span
              className={styles.bar}
              style={{
                width: ${hero.powerstats.strength}%,
                backgroundColor: "#FF7C6C",
              }}
            />
          </p>
        </article>
      ))}
    </div>
  );
}   ```



Estrutura do Código
fetchHero(id): Função para buscar dados de um herói específico pela API.
useEffect: Hook usado para buscar os dados dos heróis quando o componente é montado.
styles: Módulo de estilos CSS utilizado para personalização visual.
Componente Home: Renderiza as informações dos heróis com barras de estatísticas de poder estilizadas.
