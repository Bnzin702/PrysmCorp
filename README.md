# Prysm Corporation: site institucional

Site estático (HTML + CSS + JavaScript puro). **Não precisa de Node.js, banco de dados, servidor ou variáveis de ambiente.** Funciona em computador, Android e iOS.

## Estrutura

```
prysm-corporation/
├── index.html          # o site inteiro (páginas, estilos e scripts)
├── legal.html          # Privacidade e Termos como página avulsa
├── 404.html            # página de erro para URLs inexistentes
├── exemplos/           # os dois sites de exemplo, também abrem sozinhos
├── assets/
│   ├── logo.webp       # logo usada no site (fundo transparente)
│   ├── logo-original.jpg  # logo original enviada
│   └── favicon.svg     # ícone da aba do navegador
├── .env.example        # modelo (o site não usa variáveis hoje)
├── .gitignore
└── README.md
```

As "páginas" (Início, Sobre nós, Serviços, Como funciona, Avaliações, Patrocinadores) são seções do `index.html`, trocadas pelo menu usando o endereço com `#`: `index.html#servicos`, `#avaliacoes` etc. Por isso funciona em qualquer hospedagem, sem configurar rotas.

## O que está implementado

**Funciona sem serviços externos**
- Menu de navegação e as 6 páginas.
- Layout responsivo (computador, Android e iOS).
- Telefone clicável (`tel:`) e botão "Chamar no WhatsApp" (https://wa.me/5531989516662).
- Formulário de Serviços: valida nome e mensagem e abre o WhatsApp da empresa com o texto pronto. **Não envia e-mail e não guarda os dados**; quem envia a mensagem é o próprio visitante pelo WhatsApp.
- Visual em preto, branco e degradê cinza, com a fonte Poppins carregada do Google Fonts (precisa de internet; sem ela o navegador usa uma fonte do sistema).
- Página exclusiva “Privacidade e Termos”, com abas para os dois documentos (endereços `index.html#privacidade` e `index.html#termos`) e uma versão avulsa, `legal.html`, para você divulgar o link em redes sociais ou em formulários. Páginas “Política de Privacidade e Cookies” e “Termos de Uso” (links no rodapé), escritas com base na LGPD. **São um modelo: antes de usar com clientes, peça a revisão de um advogado e complete com CNPJ, endereço e encarregado de dados (DPO), se houver.**
- Aviso de cookies: o visitante escolhe “Aceitar todos”, “Recusar opcionais” ou “Personalizar”. Só o armazenamento funcional (avaliações salvas no navegador) depende dessa escolha. Ela pode ser mudada em “Preferências de cookies”, no rodapé.
- Os formulários só enviam depois de o visitante marcar que leu os Termos e a Política.
- Página de erro 404: endereços inexistentes dentro do site (ex.: `index.html#abc`) mostram a tela 404, e o arquivo `404.html` é usado automaticamente por Netlify, Cloudflare Pages e GitHub Pages quando alguém abre uma URL que não existe. Se você mudar o site, revise a seção de cookies da política caso passe a usar análise, anúncios ou outros serviços.
- Dois exemplos interativos em destaque na página inicial (e na aba Sobre nós): **loja de roupas** (catálogo, filtros, carrinho, checkout de teste e painel do dono com acesso de exemplo) e **oficina mecânica** (serviços, FAQ e solicitação de agendamento com validação, enviada pelo WhatsApp). Os arquivos estão em `exemplos/loja.html` e `exemplos/mecanica.html`, e também embutidos no `index.html`. Na loja, produtos, carrinho e pedidos são de teste e ficam só no navegador. Para vender de verdade, é preciso ligar a um backend (por exemplo Supabase e Mercado Pago). Os exemplos usam o WhatsApp sem número de destino.
- Acessibilidade: link “Pular para o conteúdo”, foco visível, navegação por teclado (inclusive nas estrelas e nos exemplos), mensagens anunciadas por leitores de tela e respeito a “reduzir movimento”.
- Avaliações de 1 a 5 estrelas com comentário, mostradas na aba Avaliações e na página inicial.

**Limitação importante:** as avaliações ficam salvas apenas no navegador de quem as escreveu (`localStorage`). Um visitante **não vê** as avaliações de outras pessoas.

**Não existe neste projeto (nunca foi implementado)**
- Formulário separado de parcerias (a aba Patrocinadores só direciona para o formulário de Serviços).
- Portfólio e status de disponibilidade dos serviços.
- Painel administrativo, login, banco de dados, envio de e-mail.

Se quiser algum desses itens, eles precisam ser desenvolvidos. Alguns exigem serviço externo (por exemplo Formspree/Web3Forms para formulários e Supabase/Firebase para avaliações compartilhadas).

## Executar no seu computador

1. Baixe o ZIP e extraia (clique direito, "Extrair tudo").
2. Mais simples: dê dois cliques em `index.html`. Ele abre no navegador.
3. Opcional, com servidor local (precisa de Python ou Node.js instalado):
   - `python -m http.server 8000` (dentro da pasta), depois abra http://localhost:8000
   - ou `npx serve .`

Não há `npm install` nem `.env` para configurar.

## Testar

- Clique em cada item do menu e confira se a página muda.
- Em Serviços: clique no telefone e no botão de WhatsApp; envie o formulário vazio (deve aparecer aviso) e depois preenchido (abre o WhatsApp).
- Em Avaliações: tente enviar sem nota (deve avisar), depois envie uma avaliação completa e confira o cartão e a página inicial.
- Redimensione a janela ou abra no celular para ver o layout responsivo.

## Publicar gratuitamente (hospedagem estática)

Qualquer uma serve; basta enviar a pasta:

**Netlify (mais fácil):** acesse app.netlify.com/drop e arraste a pasta `prysm-corporation`. O site recebe um endereço `.netlify.app`.

**Cloudflare Pages:** crie um projeto, escolha "Upload direto" e envie a pasta (sem comando de build).

**GitHub Pages:** crie um repositório, envie os arquivos, depois em Settings > Pages escolha a branch `main` e a pasta `/ (root)`.

Em todas, deixe vazios os campos "Build command" e "Environment variables".

## Domínio próprio

1. Registre o domínio (`.com.br` em registro.br; ou em outro registrador).
2. Na hospedagem escolhida, abra a área "Domains/Domínios" e adicione o domínio.
3. A hospedagem mostra os registros DNS (CNAME ou A) a criar; cadastre-os no painel do registrador.
4. Aguarde a propagação (de minutos a algumas horas). O certificado HTTPS é emitido automaticamente.

## Atualizar depois, sem o Claude

- Textos e seções: edite `index.html` em qualquer editor (VS Code, Bloco de Notas) e envie de novo à hospedagem. Cada página fica entre comentários como `<!-- SOBRE NÓS -->`.
- Cores: estão nas variáveis no topo do `<style>` (`--fundo`, `--marinho`, `--prata` etc.).
- Telefone: procure por `5531989516662` e `98951-6662`.
- Logo: ela está embutida dentro do `index.html` (variável `LOGO` no final do arquivo), por isso aparece mesmo se você enviar só esse arquivo. Para trocar, converta a nova imagem para base64 e substitua o valor de `LOGO`, ou peça ajuda a um desenvolvedor.

## Custos e limites

- Hospedagem estática: os planos gratuitos de Netlify, Cloudflare Pages e GitHub Pages costumam bastar para um site institucional, mas têm limites de tráfego que podem mudar. Confira nos sites deles.
- Domínio: costuma ser pago por ano (`.com.br` em geral custa poucas dezenas de reais por ano no Registro.br).
- Serviços extras (formulário por e-mail, banco de dados) têm planos gratuitos limitados e pagos acima deles.
