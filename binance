<?php
declare(strict_types=1);

namespace Thelema\Crypto;

/**
 * Singleton pattern
 *
 * @package Thelema
 */
abstract class Singleton
{
    // Hold the class instance.
    protected static $_instance;

    // Prevent initiation with outer code
    protected function __construct()
    {
    }

    // Prevent cloning with outer code
    protected function __clone()
    {
    }

    // Prevent creating instance by unserialize
    public function __wakeup()
    {
        throw new \Exception("Cannot unserialize an instance.");
    }

    // Return single class instance
    public final static function getInstance()
    {
        if (null === static::$_instance) {
            static::$_instance = new static();
        }

        return static::$_instance;
    }
}

/**
 * A simplified HTTP client for collecting cryptocurrency
 * exchange rate information
 *
 * @package Thelema
 */
final class Binance extends Singleton
{
    const API_SERVER = 'https://api.binance.com';

    const API_VERSION = '/api/v3/';

    private static $connect = null;

    /**
     * Check if server is alive
     * @return bool
     */
    public function ping(): bool
    {
        $result = false;

        static::$connect = curl_init();

        if (static::$connect) {
            $url = self::API_SERVER . self::API_VERSION . 'ping';
            curl_setopt(static::$connect, CURLOPT_RETURNTRANSFER, true);
            curl_setopt(static::$connect, CURLOPT_URL, $url);
            $result = curl_exec(static::$connect);
            return empty((array)json_decode($result));
        } else {
            return $result;
        }
    }

    /**
     *
     *
     * @param string $command
     * @param string $symbol
     * @param string $limit
     * @return array
     */
    public function get(string $command = null, string $symbol = null, int $limit = null): array
    {
        $result = '{}';
        if ($this->ping() && static::$connect) {
            $url = self::API_SERVER . self::API_VERSION . $command;

            if (!is_null($symbol) && is_null($limit)) {
                $url = $url . '?symbol=' . $symbol;
            }

            if (!is_null($symbol) && !is_null($limit)) {
                $url = $url . '?symbol=' . $symbol . '&limit=' . $limit;
            }

            curl_setopt(static::$connect, CURLOPT_RETURNTRANSFER, true);
            curl_setopt(static::$connect, CURLOPT_URL, $url);
            $result = curl_exec(static::$connect);
            curl_close(static::$connect);
        }

        return (array)json_decode($result);
    }
}
