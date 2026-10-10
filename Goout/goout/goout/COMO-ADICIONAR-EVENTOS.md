# GoOut — Como adicionar eventos (guia dos sócios)

Os eventos do site vêm de uma **planilha do Google**. Cada sócio entra com a **própria conta Google**
e o site atualiza sozinho em até 5 minutos depois de salvar.

---

## Parte A — Configuração (só o Vitor faz, uma vez)

### 1. A planilha
Já está criada no Google Drive do Vitor:
[GoOut — Eventos](https://docs.google.com/spreadsheets/d/13USa2wzpcOhFF-f6R4ZP0SKuzETC_ZyWQuqZZTtAdPo/edit)

### 2. Dar acesso aos sócios (cada um com o seu login)
1. Na planilha, clique em **Compartilhar** (canto superior direito).
2. Adicione o e-mail Google de cada sócio como **Editor**.
3. Em "Acesso geral", deixe **Restrito**. Assim só vocês 4 podem editar.

### 3. Publicar a planilha para o site conseguir ler
1. Menu **Arquivo → Compartilhar → Publicar na Web**.
2. Na primeira lista escolha a aba **Eventos**; na segunda escolha **Valores separados por vírgula (.csv)**.
3. Clique em **Publicar** e confirme. Copie o link que aparece.

> Isso deixa o site *ler* os eventos (que já são públicos de qualquer forma).
> Ninguém consegue *editar* sem ser um dos 4 editores.

### 4. Colar o link no código
1. No VS Code, abra `js/app.js`.
2. Logo no começo, em `PLANILHA_CSV_URL: ''`, cole o link entre as aspas:
   ```js
   PLANILHA_CSV_URL: 'https://docs.google.com/spreadsheets/d/e/2PACX-.../pub?gid=0&single=true&output=csv',
   ```
3. Salve e publique o site de novo (Vercel/Netlify). Pronto: daqui pra frente ninguém mexe mais no código para adicionar evento.

Se a planilha um dia falhar, o site usa automaticamente o `data/eventos.json` como reserva.

---

## Parte B — Adicionar um evento (todos os sócios)

1. Abra a planilha e vá na aba **Eventos**.
2. Preencha a **primeira linha vazia**. Uma linha = um evento.
3. Salvou, em até 5 minutos está no site.

| Coluna | O que colocar | Exemplo |
|---|---|---|
| id | Pode deixar vazio | |
| nome **\*** | Nome do evento | Noite de Jazz no Rossio |
| descricao | Texto curto, em português de Portugal | Concerto ao ar livre... |
| categoria **\*** | Escolha na lista | música |
| data_inicio **\*** | ano-mês-dia hora:minuto | 2026-11-14 21:00 |
| data_fim | Igual; vazio = 3 horas de duração | 2026-11-14 23:30 |
| local_nome **\*** | Nome do lugar | Praça do Rossio |
| endereco | Endereço completo | Praça Dom Pedro IV, Lisboa |
| latitude **\*** | 1º número do Google Maps (com ponto) | 38.7139 |
| longitude **\*** | 2º número do Google Maps (com ponto) | -9.1394 |
| cidade **\*** | Lisboa, Porto, Aveiro... | Lisboa |
| preco | Texto livre | Grátis / 10 € |
| imagem_url | Link direto de uma imagem | https://... |
| link_externo | Bilhetes ou Instagram | https://instagram.com/... |
| destaque | **sim** = aparece no carrossel do topo | não |

**\*** obrigatório. Se faltar, o evento não aparece.

### Como pegar latitude e longitude
1. Abra o [Google Maps](https://maps.google.com) e ache o local.
2. Clique com o **botão direito** exatamente em cima do local.
3. O primeiro item do menu são dois números, ex.: `38.7139, -9.1394`. Clique nele para copiar.
4. O primeiro número vai em **latitude**, o segundo em **longitude**.

### Regras rápidas
- **Não mude os títulos laranja** da primeira linha. O site usa esses nomes.
- Para tirar um evento do site, **apague a linha inteira**.
- Eventos que já terminaram **somem sozinhos**. Não precisa apagar.
- No máximo **4 destaques** aparecem no carrossel (os mais próximos).
- Textos do site em **português de Portugal**: bilhetes, desporto, grátis, "Descobre".
