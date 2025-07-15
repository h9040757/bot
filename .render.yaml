const { default: makeWASocket, useSingleFileAuthState } = require("@whiskeysockets/baileys");
const { Boom } = require("@hapi/boom");
const { state, saveState } = useSingleFileAuthState("./auth.json");
const fs = require("fs");

async function connect() {
  const sock = makeWASocket({ auth: state });
  sock.ev.on("creds.update", saveState);
  sock.ev.on("connection.update", ({ connection }) => {
    if (connection === "open") console.log("✅ Connected to WhatsApp");
    if (connection === "close") console.log("❌ Disconnected");
  });

  // Example: Send message every 10 minutes (test only)
  setInterval(() => {
    const number = "91XXXXXXXXXX@s.whatsapp.net"; // your group or self-chat ID
    sock.sendMessage(number, { text: "🛫 Automated flight update sent from Render!" });
  }, 600000);
}

connect();
