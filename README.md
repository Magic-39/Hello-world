
pragma solidity ^0.4.11;

//Подключаем библиотеку

import "github.com/oraclize/ethereum-api/oraclizeAPI.sol";

//Объявляем контракт

contract DollarCost is usingOraclize{

//Устанавливаем переменную для хранения курса доллара
   
   uint public dollarCost;
    
    //В эту функцию отдадут результат
   
  function __callback(bytes32 myid, string result){
    
    //проверяем, что функцию вызывает ораклайзер
   
   if (msg.sender != oraclize_cbAddress()) throw; 
    
    //Обновляем переменную курса доллара
   
   dollarCost = parseInt(result, 3);
    }
    
     //(функция вызова ораклайзера)
    
   function updatePrise() public payable {
       
       //Проверка наличия ср-в для оплаты ораклайзера
      
   if (oraclize_getPrice("URL") > this.balance){ 
       
       //если ср-в не хватило, завершаем выполнение
       
   return;
    }
        
   
   else{
         
        //Если ср-в хватило, отправляем запрос в ораклайзер
       
   oraclize_query("URL", "json(https://api.kraken.com/0/public/Ticker?pair=ETHUSD), result.XETHZUSD.c.[0]");
  }
 }
}

