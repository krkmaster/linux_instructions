#  Setup Redis for Opencart 3
нужно прописать константы в config.php и admin/config.php:

    define('CACHE_HOSTNAME', '127.0.0.1');
    define('CACHE_PORT', '6379');
    define('CACHE_PREFIX', 'ocredis_');


И в настройках по умолчанию system/config/default.php указать движок для кэша


    $['cache_engine']         = 'redis'; // apc, file, mem or memcached


С сессиями оказалось чуть сложнее, так как механизм сессий у opencart свой и настройка в php никак 
не влияет на неё. 
По умолчанию админка хранит сессии в файлах, фронт часть хранит в БД и эти 2 драйвера доступны, 
но нам надо в redis.

Для этого был написан простенький класс system/library/session/redis.php:


    <?php
    /**
    * Author: Shabalin Pavel
    */
 
    namespace Session;
 
 
    final class Redis
    {
    public $expire = '';
    protected $prefix = 'sess_';
 
    public function __construct($registry)
    {
        $this->redis = new \Redis();
 
        if (!$this->redis->pconnect('127.0.0.1')) {
            throw new \Exception("Permissions denied session storage");
        }
 
        $this->expire = ini_get('session.gc_maxlifetime');
    }
 
    public function read($session_id)
    {
        if ($this->redis->exists($this->prefix . $session_id)) {
            return json_decode( $this->redis->get($this->prefix . $session_id), true );
        }
 
        return false;
    }
 
    public function write($session_id, $data)
    {
        if ($session_id) {
            $this->redis->psetex($this->prefix . $session_id, $this->expire * 1000, json_encode($data));
        }
 
        return true;
    }
 
    public function destroy($session_id)
    {
        if ($this->redis->exists($this->prefix . $session_id)) {
            $this->redis->delete($this->prefix . $session_id);
        }
 
        return true;
    }
 
    public function gc($expire) {
        return true;
    }
 
    }


И поменять настройки для фронт и бэк части system/config/catalog.php и system/config/admin.php:


    // Session
    $_['session_engine']       = 'redis';
