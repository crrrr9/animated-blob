HERE'S HOW IT LOOKS
https://github.com/user-attachments/assets/b649a8d5-d7ec-4c89-a636-9a6115421fb7
import { useState } from "react";
import "./App.css";
import scLogo from "./sc-logo.png";
//npm npm install jspdf
const usersData = [
  {
    name: "Shraddha",
    accounts: [
      { name: "Savings Acc.", number: "XXXX1234", type: "Savings", currency: "USD", balance: 5000, bankingSegment: "Personal Banking" },
      { name: "Checking Acc.", number: "XXXX5678", type: "Checking", currency: "USD", balance: 2300, bankingSegment: "Personal Banking" },
      { name: "NRI Account", number: "XXXX9999", type: "NRI", currency: "INR", balance: 150000, bankingSegment: "NRI Banking" },
    ],
  },
  {
    name: "Virat",
    accounts: [
      { name: "Wealth Savings", number: "XXXX1111", type: "Savings", currency: "USD", balance: 75000, bankingSegment: "Priority Banking" },
      { name: "Wealth Investment", number: "XXXX3333", type: "Investment", currency: "USD", balance: 120000, bankingSegment: "Priority Banking" },
      { name: "Business Account", number: "XXXX2222", type: "Business", currency: "GBP", balance: 50000, bankingSegment: "Business Banking" },
    ],
  },
  {
    name: "Amit",
    accounts: [
      { name: "Personal Savings", number: "XXXX4444", type: "Savings", currency: "EUR", balance: 9000, bankingSegment: "Personal Banking" },
      { name: "Business Checking", number: "XXXX5555", type: "Checking", currency: "USD", balance: 12000, bankingSegment: "Business Banking" },
    ],
  },
];
 
const transactionsData = [
  { date: "2025-08-01", description: "ATM Withdrawal", debit: 200, credit: "-", balance: 4800 },
  { date: "2025-07-28", description: "Salary Credit", debit: "-", credit: 3000, balance: 5000 },
  { date: "2025-07-20", description: "Utility Bill Payment", debit: 150, credit: "-", balance: 2000 },
  { date: "2025-07-15", description: "Transfer from John", debit: "-", credit: 800, balance: 2150 },
  { date: "2025-07-10", description: "Online Shopping", debit: 120, credit: "-", balance: 1350 },
  { date: "2025-06-30", description: "Interest Credit", debit: "-", credit: 50, balance: 1400 },
  { date: "2025-06-25", description: "Mobile Recharge", debit: 20, credit: "-", balance: 1350 },
  { date: "2025-06-20", description: "Transfer to Amit", debit: 500, credit: "-", balance: 850 },
  { date: "2025-06-15", description: "Cheque Deposit", debit: "-", credit: 1000, balance: 1850 },
  { date: "2025-06-10", description: "Dining", debit: 60, credit: "-", balance: 1790 },
  { date: "2025-06-05", description: "Business Income", debit: "-", credit: 5000, balance: 6790 },
  { date: "2025-05-30", description: "Travel Expense", debit: 300, credit: "-", balance: 6490 },
  { date: "2025-05-25", description: "Gift Received", debit: "-", credit: 200, balance: 6690 },
  { date: "2025-05-20", description: "Loan EMI", debit: 1000, credit: "-", balance: 5690 },
  { date: "2025-05-15", description: "Transfer from Virat", debit: "-", credit: 1500, balance: 7190 },
];
 
const exchangeRates = {
  USD: { rate: 1, symbol: "$" },
  EUR: { rate: 0.92, symbol: "€" },
  GBP: { rate: 0.79, symbol: "£" },
  INR: { rate: 83, symbol: "₹" },
};
 
function App() {
  const [selectedAccount, setSelectedAccount] = useState(null);
  const [search, setSearch] = useState("");
  const [bankingType, setBankingType] = useState("Personal Banking");
    const [showTxModal, setShowTxModal] = useState(false);
    const [modalTx, setModalTx] = useState(null);
  const [currency, setCurrency] = useState({});
  const [fromDate, setFromDate] = useState("");
  const [toDate, setToDate] = useState("");
  const [currentUser, setCurrentUser] = useState(usersData[0]);
 
  const filteredAccounts = currentUser.accounts
    .filter(acc => acc.bankingSegment === bankingType)
    .filter(acc => acc.name.toLowerCase().includes(search.toLowerCase()));
 
  const filteredTransactions = () => {
    return transactionsData.filter(t => {
      const txDate = new Date(t.date);
      const from = fromDate ? new Date(fromDate) : null;
      const to = toDate ? new Date(toDate) : null;
      return (!from || txDate >= from) && (!to || txDate <= to);
    });
  };
 
  const handleDownload = (type) => {
    let content = "Date,Description,Debit,Credit,Balance\n";
    filteredTransactions().forEach(t => {
      content += `${t.date},${t.description},${t.debit},${t.credit},${t.balance}\n`;
    });
    if (type === "pdf") {
      // Use jsPDF to generate a real PDF
      import("jspdf").then(jsPDFModule => {
        const jsPDF = jsPDFModule.default;
        const doc = new jsPDF();
        doc.text("Date, Description, Debit, Credit, Balance", 10, 10);
        let y = 20;
        filteredTransactions().forEach(t => {
          doc.text(`${t.date}, ${t.description}, ${t.debit}, ${t.credit}, ${t.balance}`, 10, y);
          y += 10;
        });
        doc.save("statement.pdf");
      });
    } else {
      const blob = new Blob([content], { type: "text/csv" });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "statement.csv";
      link.click();
    }
  };
 
  const switchUser = (user) => {
    setCurrentUser(user);
    setSelectedAccount(null);
  };
 
  return (
    <div className="app">
      <div className="background-effects">
        <div className="background-image"></div>
        <div className="background-overlay"></div>
      </div>
 
      <header className="header">
        <div className="header-left">
          { <img src={scLogo} alt="Standard Chartered" className="logo" /> }
          <select value={bankingType} onChange={(e) => { setBankingType(e.target.value); setSelectedAccount(null); setShowTxModal(false); }} className="banking-dropdown">
            <option>Priority Banking</option>
            <option>Personal Banking</option>
            <option>NRI Banking</option>
            <option>Business Banking</option>
          </select>
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
            <select className="user-switcher" onChange={(e) => switchUser(usersData[e.target.value])}>
              {usersData.map((u, idx) => (
                <option key={idx} value={idx}>{u.name}</option>
              ))}
            </select>
          </div>
        </div>
      </header>
 
      <div className="account-overview">
        <h2>Account Position</h2>
        <table>
          <thead>
            <tr>
              <th>Account Name</th>
              <th>Account No.</th>
              <th>Type</th>
              <th>Currency</th>
              <th>Balance</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            {filteredAccounts.map((acc, index) => (
              <tr key={index}>
                <td>{acc.name}</td>
                <td>{acc.number}</td>
                <td>{acc.type}</td>
                <td>
                  <select
                    value={currency[acc.number] || acc.currency}
                    onChange={(e) =>
                      setCurrency({ ...currency, [acc.number]: e.target.value })
                    }
                  >
                    {Object.keys(exchangeRates).map(cur => (
                      <option key={cur}>{cur}</option>
                    ))}
                  </select>
                </td>
                <td>
                  {exchangeRates[currency[acc.number] || acc.currency].symbol}
                  {(acc.balance * exchangeRates[currency[acc.number] || acc.currency].rate).toLocaleString()}
                </td>
                <td>
                  <button onClick={() => setSelectedAccount(acc)}>View Transactions</button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
 
      <div className="transactions">
        <h2>Transactions</h2>
        {selectedAccount ? (
          <>
            <div className="top-bar">
              <input type="date" value={fromDate} onChange={(e) => setFromDate(e.target.value)} /> to
              <input type="date" value={toDate} onChange={(e) => setToDate(e.target.value)} />
              <button onClick={() => { setFromDate(""); setToDate(""); }}>Clear Dates</button>
              <button onClick={() => handleDownload("csv")}>Download CSV</button>
              <button onClick={() => handleDownload("pdf")}>Download PDF</button>
            </div>
            <table>
              <thead>
                <tr>
                  <th>Date</th>
                  <th>Description</th>
                  <th>Debit</th>
                  <th>Credit</th>
                  <th>Balance</th>
                    <th>Details</th>
                </tr>
              </thead>
              <tbody>
                {filteredTransactions().length > 0 ? (
                  filteredTransactions().map((t, index) => (
                    <tr key={index}>
                      <td>{t.date}</td>
                      <td>{t.description}</td>
                      <td>{t.debit !== "-" ? `$${t.debit}` : "-"}</td>
                      <td>{t.credit !== "-" ? `$${t.credit}` : "-"}</td>
                      <td>{`$${t.balance}`}</td>
                        <td>
                          <button
                            style={{ background: "none", border: "none", cursor: "pointer" }}
                            title="View Details"
                            onClick={() => { setModalTx(t); setShowTxModal(true); }}
                          >
                            <span role="img" aria-label="eye">👁️</span>
                          </button>
                        </td>
                    </tr>
                  ))
                ) : (
                  <tr>
                    <td colSpan="5" style={{ color: "gray", fontStyle: "italic" }}>
                      No transactions found for the selected date range.
                    </td>
                  </tr>
                )}
              </tbody>
            </table>
          </>
        ) : (
          <p style={{ color: "gray", fontStyle: "italic" }}>
            Select an account to view transactions.
          </p>
        )}
      </div>
        {showTxModal && modalTx && (
          <div style={{
            position: "fixed",
            top: 0,
            left: 0,
            width: "100vw",
            height: "100vh",
            background: "rgba(0,0,0,0.4)",
            display: "flex",
            alignItems: "center",
            justifyContent: "center",
            zIndex: 9999
          }} onClick={() => setShowTxModal(false)}>
            <div style={{
              background: "#fff",
              padding: "2rem",
              borderRadius: "8px",
              minWidth: "300px",
              boxShadow: "0 2px 8px rgba(0,0,0,0.2)",
              position: "relative"
            }} onClick={e => e.stopPropagation()}>
              <h3 style={{marginTop:0}}>Transaction Details</h3>
              <p><strong>Date:</strong> {modalTx.date}</p>
              <p><strong>Description:</strong> {modalTx.description}</p>
              <p><strong>Debit:</strong> {modalTx.debit !== "-" ? `$${modalTx.debit}` : "-"}</p>
              <p><strong>Credit:</strong> {modalTx.credit !== "-" ? `$${modalTx.credit}` : "-"}</p>
              <p><strong>Balance:</strong> {`$${modalTx.balance}`}</p>
              <button style={{position:"absolute",top:10,right:10}} onClick={() => setShowTxModal(false)}>Close</button>
            </div>
          </div>
        )}
    </div>
  );
}
 
export default App;
