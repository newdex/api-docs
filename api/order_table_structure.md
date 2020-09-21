# Newdex Smart Contract API

## Exchange pair table structure

```
struct ndx_symbol {
    name contract;
    symbol sym;
};

TABLE exchange_pair {
    uint64_t pair_id;               //ID
    uint8_t price_precision;   
    uint8_t status;                 //status：0 normal 1 pause 2 delisting 3 delisted
    ndx_symbol base_symbol;  
    ndx_symbol quote_symbol; 
    name manager;                 
    time_point_sec list_time;    
    string pair_symbol;           //for example：newdexissuer-ndx-eos
    double current_price;        
    uint64_t base_currency_id;   
    uint64_t quote_currency_id; 
    uint8_t pair_fee;                  
    uint64_t ext1;                     
    uint64_t ext2;                     
    string extstr;                      

    uint64_t primary_key() const { return pair_id; }
    uint64_t pair_key() const { return uint64_hash( pair_symbol ); }
    uint128_t get_currency_id() const { return ((uint128_t)base_currency_id << 64) + quote_currency_id; }

    EOSLIB_SERIALIZE( exchange_pair, (pair_id)(price_precision)(status)(base_symbol)(quote_symbol)(manager)(list_time)(pair_symbol)(current_price)(base_currency_id)(quote_currency_id)(pair_fee)(ext1)(ext2)(extstr) )
};
```

## Currency table structure
```
TABLE currency {
    uint64_t currency_id;     
    string chain;               //for example：eos，bos
    name contract;           
    symbol sym;               
    asset balance;             
    bool is_quote_currency; 
    uint8_t in_fee;             
    uint8_t out_fee;           
    uint64_t ext1;             
    uint64_t ext2;             
    string extstr;              

    uint64_t primary_key() const { return currency_id; }
    uint128_t get_contract() const { return ((uint128_t)contract.value << 64) + sym.code().raw(); }

    EOSLIB_SERIALIZE( currency, (currency_id)(chain)(contract)(sym)(balance)(is_quote_currency)(in_fee)(out_fee)(ext1)(ext2)(extstr) )
};
```

## Order table structure

```
TABLE order {
    uint64_t order_id;                  //order ID
    uint64_t pair_id;                    //pair ID
    uint8_t type;                          //order type, 1:limit-buy  2:limit-sell  3:market-buy  4:market-sell
    name owner;                          
    time_point_sec placed_time;     
    asset remain_quantity;             
    asset remain_convert;                
    double price;                        
    name contract;                        // token contract        
    uint8_t count;                         //transfer count
    uint8_t crosschain;                  // is crosschain
    uint64_t ext1;                          
    string extstr;                       

    uint64_t primary_key() const { return order_id; }
    uint128_t get_price() const {
        uint64_t max = 1000000000000;
        if ( type == INT_BUY_LIMIT || type  == INT_BUY_MARKET ) {
            uint128_t high = (uint128_t)(max * price);
            uint64_t low = max - placed_time.utc_seconds;
            uint128_t price128 = (high << 64) + low;
            return price128;
        } else {
            return (uint128_t)(max * price);
        }
    }
    uint64_t get_name() const { return owner.value; }

    EOSLIB_SERIALIZE( order, (order_id)(pair_id)(type)(owner)(placed_time)(remain_quantity)(remain_convert)(price)(contract)(count)(crosschain)(ext1)(extstr) )
};
  ```
  
## Index
  
```
typedef eosio::multi_index<"buyorder"_n, order,
  indexed_by< "byprice"_n, const_mem_fun<order, uint128_t, &order::get_price> >,
  indexed_by< "byname"_n, const_mem_fun<order, uint64_t, &order::get_name> >
  > buy_order_t;
  typedef eosio::multi_index<"sellorder"_n, order,
  indexed_by< "byprice"_n, const_mem_fun<order, uint128_t, &order::get_price> >,
  indexed_by< "byname"_n, const_mem_fun<order, uint64_t, &order::get_name> >
  > sell_order_t;
```

## helper functions
```
uint64_t uint64_hash(const string& hash) {
    return std::hash<string>{}(hash);
}
```
  
## Use
  
```
buy_order_t buy_table("newdexpublic"_n, 235);  // newdexissuer-ndx-eos
auto buy_price_index = buy_table.get_index<"byprice"_n>();
// get all buy orders by price
while (buy_price_index.begin() !== buy_price_index.end()) {
  // do something
}
```
  
