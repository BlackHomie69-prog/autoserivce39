
export default {
  async fetch(request, env) {
    if (request.method !== "POST") {
      return new Response("Autoservice39 работает!");
    }

    const update = await request.json();
    const message = update.message;

    if (!message) return new Response("OK");

    const chatId = message.chat.id;
    const userText = message.text || "";

    let answer;

    if (userText === "/start") {
      answer = "🚗 Добро пожаловать в автосервис Karapetyan!\n\nМы выполняем:\n🔧 Кузовной ремонт\n🎨 Покраску\n⚡ Сварку\n✨ Полировку\n\nНапишите ваше имя и номер телефона, чтобы оставить заявку.";
    } else {
      answer = "✅ Спасибо! Ваша заявка принята. Мастер свяжется с вами.";
      
      await fetch(
        `https://api.telegram.org/bot${env.BOT_TOKEN}/sendMessage`,
        {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            chat_id: env.ADMIN_CHAT_ID,
            text: "📩 НОВАЯ ЗАЯВКА AUTOSERVICE39\n\n" + userText
          })
        }
      );
    }

    await fetch(
      `https://api.telegram.org/bot${env.BOT_TOKEN}/sendMessage`,
      {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          chat_id: chatId,
          text: answer
        })
      }
    );

    return new Response("OK");
  }
};
