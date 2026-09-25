export default async function handler(req, res) {
  if (req.method !== "POST") {
    return res.status(405).json({ error: "POST requests only" });
  }

  try {
    const { prompt } = req.body;

    if (!prompt) {
      return res.status(400).json({ error: "Please enter a video prompt." });
    }

    const response = await fetch(
      "https://api.evolink.ai/v1/videos/generations",
      {
        method: "POST",
        headers: {
          "Authorization": `Bearer ${process.env.EVOLINK_API_KEY}`,
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          model: "wan2.7-text-to-video",
          prompt: prompt,
          quality: "720p",
          aspect_ratio: "16:9",
          duration: 5
        })
      }
    );

    const data = await response.json();

    return res.status(response.status).json(data);
  } catch (error) {
    return res.status(500).json({
      error: "Something went wrong.",
      details: error.message
    });
  }
}
