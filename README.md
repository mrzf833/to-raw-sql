# to-raw-sql

## Tambahkan kode ini ke app/providers/AppServicesProvider tambahkan di funtion boot()
         \Illuminate\Database\Query\Builder::macro('toRawSql', function(){
            return array_reduce($this->getBindings(), function($sql, $binding){
                return preg_replace('/\?/', is_string($binding) ? "'".$binding."'" : $binding , $sql, 1);
            }, $this->toSql());
        });

        \Illuminate\Database\Eloquent\Builder::macro('toRawSql', function(){
            return ($this->getQuery()->toRawSql());
        });

## cara penggunanaannya tinggal pakai toRawSql()
User::all()->toRawSql();
