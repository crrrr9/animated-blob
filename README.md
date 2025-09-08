localhost:8080/api/company_accounts/balance


package com.scb.Payment.Initiation.controller;
import com.scb.Payment.Initiation.entity.CompanyAccounts;
import com.scb.Payment.Initiation.service.CompanyAccountService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/company_accounts")
public class CompanyAccountController {

    private final CompanyAccountService service;

    public CompanyAccountController(CompanyAccountService service){
        this.service = service;
    }

    //creation fo the account




    @PostMapping("/create")
    public CompanyAccounts create(@RequestBody CompanyAccounts account){
        return service.createAccount(account);
    }

    @GetMapping //to fetch all accounts
    public List<CompanyAccounts> getAll(){
        return service.getAllAccounts();
    }


    //fetch by id
    @GetMapping("/{id}")
    public CompanyAccounts getById(@PathVariable Long id){
        return service.getAccountById(id);
    }


    @PutMapping("/{id}")
    public CompanyAccounts update(@PathVariable Long id,@RequestBody CompanyAccounts account)
    {
        return service.updateAccount(id,account);
    }

    @GetMapping("/balance")
    public Double getBalance() {
        return service.getBalance();
    }



}




package com.scb.Payment.Initiation.service;
import com.scb.Payment.Initiation.entity.CompanyAccounts;
import com.scb.Payment.Initiation.repository.CompanyAccountRepository;
import org.springframework.stereotype.Service;
import java.util.List;

@Service
public class CompanyAccountService {

    private final CompanyAccountRepository repository;

    public CompanyAccountService(CompanyAccountRepository repository){
        this.repository=  repository;
    }

    //creation of an account

    public CompanyAccounts createAccount(CompanyAccounts account){
        return repository.save(account);
    }

    //fetching all the accounts to display

    public List<CompanyAccounts> getAllAccounts(){
        return repository.findAll();
    }
    public CompanyAccounts getAccount(){
        return repository.findAll().stream().findFirst()
                .orElse(null);
    }

    //fetching by id

    public CompanyAccounts getAccountById(Long id){
        return repository.findById(id).orElse(null);
    }

// update account

    public CompanyAccounts updateAccount(Long id,CompanyAccounts updatedAccount)
    {
        return repository.findById(id).map(existingAccount->{
            existingAccount.setIfsc(updatedAccount.getIfsc());
            existingAccount.setAccountNo(updatedAccount.getAccountNo());
            existingAccount.setBank(updatedAccount.getBank());
            existingAccount.setBranch(updatedAccount.getBranch());
            return repository.save(existingAccount);
        }).orElse(null);
    }
    // fetch only balance of a companyaccount by id
    public Double getBalance() {
        return getAccount().getBalance();
    }
}





function Headerrr({  search, setSearch, currentUser, usersData, switchUser, setSelectedAccount, setShowTxModal }) 
{
  return (
    <header className="header">
      <div className="header-left">
        
          <button> view balance</button> 
          
        </div>

       
       
        
         <div className="header-right">
        <select className="country-dropdown">
          <option>India</option>
          <option>USA</option>
          <option>UK</option>
          <option>Singapore</option>
        </select>

        <input
          type="text"
          placeholder="Search account..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
          className="search-bar"
        />

        <div className="profile">
          <div className="avatar">{currentUser.name[0]}</div>
          <span className="username">{currentUser.name}</span>
          <select
            className="user-switcher"
            value={usersData.findIndex((u) => u.name === currentUser.name)}
            onChange={(e) => switchUser(usersData[e.target.value])}
          >
            {usersData.map((u, idx) => (
              <option key={idx} value={idx}>
                {u.name}
              </option>
            ))}
          </select>
        </div>
      </div>
      
      
    </header>
  );
}

export default Headerrr;
