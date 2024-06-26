## 附录 A. 从 Ownable 继承的 SimpleCoin

##### 列表 A.1\. 从`Ownable`继承的`SimpleCoin`合约重构版

```
pragma solidity ⁰.4.16;
pragma solidity ⁰.4.24;

import "./Listing6_4_Ownable.sol";

contract SimpleCoin is Ownable {                             *1*
   mapping (address => uint256) public coinBalance;
   mapping (address => mapping (address => uint256)) public allowance;
   mapping (address => bool) public frozenAccount;

   event Transfer(address indexed from, address indexed to, uint256 value);
   event FrozenAccount(address target, bool frozen);

   constructor(uint256 _initialSupply) public {
      owner = msg.sender;

      mint(owner, _initialSupply);
   }

   function transfer(address _to, uint256 _amount) public {
     require(_to != 0x0); 
     require(coinBalance[msg.sender] > _amount);
     require(coinBalance[_to] + _amount >= coinBalance[_to] );
     coinBalance[msg.sender] -= _amount;  
     coinBalance[_to] += _amount;   
     emit Transfer(msg.sender, _to, _amount);  
   }

   function authorize(address _authorizedAccount, uint256 _allowance) 
     public returns (bool success) {
     allowance[msg.sender][_authorizedAccount] = _allowance; 
     return true;
   }

   function transferFrom(address _from, address _to, uint256 _amount) 
     public returns (bool success) {
     require(_to != 0x0);  
     require(coinBalance[_from] > _amount); 
     require(coinBalance[_to] + _amount >= coinBalance[_to] ); 
     require(_amount <= allowance[_from][msg.sender]);  
     coinBalance[_from] -= _amount; 
     coinBalance[_to] += _amount; 
     allowance[_from][msg.sender] -= _amount;
     emit Transfer(_from, _to, _amount);
     return true;
   }

   function mint(address _recipient, uint256  _mintedAmount) 
     onlyOwner public { 

     coinBalance[_recipient] += _mintedAmount; 
     emit Transfer(owner, _recipient, _mintedAmount); 
   }

   function freezeAccount(address target, bool freeze) 
     onlyOwner public { 

     frozenAccount[target] = freeze;  
     emit FrozenAccount(target, freeze);
   }
}
```

+   ***1*** **`SimpleCoin`合约的拥有者状态变量和`onlyOwner`修改器是从`Ownable`合约继承来的。**
