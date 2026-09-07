# Segundas vias GLENCORE — deploy na Vercel

Este projeto tem:
- `index.html` — a app (login, gerador de tickets, histórico partilhado)
- `api/tickets.js` — a API que guarda e lista o histórico de tickets
- `package.json` — dependência da base de dados (Vercel KV)

Depois de publicado na Vercel, **todos os utilizadores** (Jossefa, Elton, Marcelo, Andrea) vêem o mesmo histórico de tickets, em tempo real, a partir de qualquer dispositivo — já não depende de estarem a usar o Claude.

---

## O que precisa de ter

1. Uma conta grátis em **https://vercel.com** (pode entrar com GitHub, GitLab, Google ou email).
2. Nada mais para já — a base de dados (Vercel KV) cria-se dentro do próprio painel da Vercel, também grátis no plano Hobby.

---

## Opção A — Deploy mais rápido (sem GitHub), usando a linha de comandos

Se tiver Node.js instalado no seu computador:

1. Abra um terminal dentro desta pasta do projeto.
2. Instale a ferramenta da Vercel (só precisa fazer isto uma vez):
   ```
   npm install -g vercel
   ```
3. Faça login:
   ```
   vercel login
   ```
4. Faça o deploy:
   ```
   vercel
   ```
   Responda às perguntas com as opções por omissão (Enter, Enter, Enter...). No final, a Vercel dá-lhe um link (ex: `https://segundas-vias-glencore.vercel.app`).
5. Siga para a secção **"Ativar a base de dados (Vercel KV)"** abaixo — é o único passo que falta.

---

## Opção B — Deploy pelo GitHub (recomendado se quiser continuar a editar o projeto no futuro)

1. Crie um repositório novo no GitHub e envie estes ficheiros para lá (`git init`, `git add .`, `git commit -m "primeira versão"`, `git push`).
2. Em **vercel.com** → **Add New... → Project** → escolha esse repositório do GitHub.
3. Deixe as definições por omissão e clique em **Deploy**.
4. Siga para a secção seguinte para ativar a base de dados.

---

## Ativar a base de dados (Vercel KV) — passo obrigatório

Sem isto, a app funciona (login, gerar PDF), mas o **histórico partilhado** não guarda nada.

1. No painel do seu projeto na Vercel, abra o separador **Storage**.
2. Clique em **Create Database** → escolha **KV** (Redis).
3. Dê um nome (ex: `tickets-db`) e confirme.
4. Na página da base de dados, clique em **Connect Project** e selecione este projeto.
5. Isto cria automaticamente as variáveis de ambiente necessárias (`KV_REST_API_URL`, `KV_REST_API_TOKEN`, etc.) — não precisa de copiar nada à mão.
6. Volte ao separador **Deployments** do projeto e clique nos "..." do último deploy → **Redeploy** (para a app arrancar já com a base de dados ligada).

---

## Pronto

Aceda ao link que a Vercel deu (ex: `https://segundas-vias-glencore.vercel.app`), faça login com um dos utilizadores, gere um ticket, e veja-o aparecer no histórico. Peça a outra pessoa para abrir o mesmo link noutro telemóvel/computador — vai ver o mesmo histórico.

---

## Notas importantes

- **O login continua a ser feito no browser** (tal como antes) — é uma barreira simples, não segurança "a sério". Isso pode ser reforçado mais tarde movendo a verificação para o servidor, se quiser.
- O plano gratuito da Vercel e do Vercel KV chega perfeitamente para este uso (poucos utilizadores, poucos tickets por dia).
- Se mudar de ideias sobre o design ou os campos do ticket mais tarde, basta editar `index.html` e voltar a fazer deploy (`vercel` outra vez, ou `git push` se estiver a usar GitHub).
