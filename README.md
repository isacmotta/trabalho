#bot_telegram 
// Importar o módulo do Telegram
const Telegram = require("telegram-bot-api");

// Definir o idioma do bot
const LANG = "pt-BR";

// Definir a senha do bot
const PASSWORD = "JOCKERD21BR";

// Definir o token do bot
const TOKEN = "6943994561:AAHdUYOQ22CEmlKzO9do2e1OQWATDiobs6E";

// Definir o nome do bot
const BOT_NAME = "JOCKERD21BULO";

// Criar uma instância do bot
const bot = new Telegram(TOKEN);

// Definir o manipulador de mensagens
bot.on("message", async (msg) => {
  // Verificar se a mensagem é um link
  if (msg.text.startsWith("https://")) {
    // Extrair o nome do bot do link
    const botName = msg.text.split("/")[3];

    // Verificar se a mensagem contém a senha
    if (msg.text.includes(PASSWORD)) {
      // Perguntar ao usuário quantos perfis ele quer criar
      const amount = await bot.sendMessage(msg.chat.id, "Quantos perfis você quer criar?");

      // Criar os perfis
      for (let i = 0; i < amount; i++) {
        // Gerar um nome aleatório
        const name = Math.random().toString(36).substring(7);

        // Gerar características aleatórias
        const characteristics = {
          age: Math.floor(Math.random() * 100),
          gender: ["masculino", "feminino"][Math.floor(Math.random() * 2)],
          location: ["São Paulo", "Rio de Janeiro", "Belo Horizonte"][Math.floor(Math.random() * 3)],
        };

        // Criar o perfil
        const profile = {
          name,
          characteristics,
        };

        // Enviar o perfil para o outro bot
        await bot.sendMessage(botName, JSON.stringify(profile));
      }
    } else {
      // Enviar uma mensagem de erro
      await bot.sendMessage(msg.chat.id, "Senha incorreta.");
    }
  }
});

// Iniciar o bot
bot.start();
