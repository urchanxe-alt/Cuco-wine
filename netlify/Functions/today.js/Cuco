const BIN_ID = "6a4382d0f5f4af5e2946517d";
const BIN_KEY = "$2a$10$3nTA/Sch04EHuUwpp0DTD.XIk/2L9G4nlhCuDaEnsDKjuASlVRZYK";

exports.handler = async function(event) {
  const headers = {
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Headers": "Content-Type",
    "Content-Type": "application/json"
  };

  if (event.httpMethod === "OPTIONS") {
    return { statusCode: 200, headers, body: "" };
  }

  if (event.httpMethod === "GET") {
    const res = await fetch("https://api.jsonbin.io/v3/b/" + BIN_ID + "/latest", {
      headers: { "X-Master-Key": BIN_KEY, "X-Bin-Meta": "false" }
    });
    const data = await res.json();
    const list = Array.isArray(data) ? data : (data.today || []);
    return { statusCode: 200, headers, body: JSON.stringify(list) };
  }

  if (event.httpMethod === "PUT") {
    const body = JSON.parse(event.body);
    const res = await fetch("https://api.jsonbin.io/v3/b/" + BIN_ID, {
      method: "PUT",
      headers: { "Content-Type": "application/json", "X-Master-Key": BIN_KEY },
      body: JSON.stringify({ today: body })
    });
    const data = await res.json();
    return { statusCode: 200, headers, body: JSON.stringify(data) };
  }

  return { statusCode: 405, headers, body: "Method not allowed" };
};
