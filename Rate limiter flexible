const { RateLimiterRedis } = require('rate-limiter-flexible');
const redis = require('redis');
const redisClient = redis.createClient();

const rateLimiter = new RateLimiterRedis({
  storeClient: redisClient,
  points: 10, // 10 requests
  duration: 1, // per second
});

app.use(async (req, res, next) => {
  try {
    await rateLimiter.consume(req.ip);
    next();
  } catch (err) {
    res.status(429).send('Too Many Requests');
  }
});
