pragma solidity ^0.4.11;

contract LessSimpleContract {


    //Переменная donator хранит значение типа Адрес
    
    address public donator;
    
    //Переменная owner, в которой будет храниться имя владельца смарт контракта.
    
    address public owner;
    
    //Переменная value, которая содержит купленное пользователем значение.
    
    uint public value;

    //Объявляем переменную LastTimeForDonate - время последней отправки средств в смарт-контракт. 
    
    uint public LastTimeForDonate;
    
    //Объявляем переменную LastTimeForValue - время последней отправки значения в смарт-контракт. 
    
    uint public LastTimeForValue;
    
    //Объявляем переменную timeOut - в которой хранится заранее определённое значение-120 секунд.
    
    uint timeOut = 120 seconds;
    
    //Функцйия инициализации смарт контракта
    
    function LessSimpleContract(){

        //Присваевается в значение owner - адрес того, кто задеплоил смарт контракт.
        
        owner = msg.sender;
    }
    
    //Функция для приёма эфиров
    
    function () payable{
    
    //внутри этой функции:
        //Проверяем, что пришло достаточне кол-во эфиров.
        
        require(msg.value > 1 finney);
        
        //Проверяем, что выполнено условие по времени.
        
        require(LastTimeForDonate + timeOut < now);
        
        //Вызываем внутрюннюю функцию
       
       setDonator(msg.sender);
    }

    //Функция для приёма эфиров и приёма какого либо значения, и установки в ранее объявленную переменную
    
    function buyValue(uint _value) payable { 
        
        //Проверяем, что пришло достаточне кол-во эфиров.
        
        require(msg.value > 1 finney);
        
        //Проверяем, что выполнено условие по времени.
       
       require(LastTimeForValue + timeOut < now);
       
       //Вызываем внутрюннюю функцию.
       
       setValue (_value);
    }
    
        //Функция установки нового значения
            
    function setValue(uint _value) internal {
    
                //внутри функции будет присваиваться переданное нами значение. 
                //происходит установка нового времени переданного значения value.
        value = _value;
        LastTimeForValue = now;
    }
        //Функция установки нового адреса donator
            
    function setDonator(address _donator) internal{
    
                //внутри функции будет присваиваться переданное нами значение. 
                //происходит установка нового времени переданного адреса donator.
                
        donator = _donator;
        LastTimeForDonate = now;
    }
}

