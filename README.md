const [balance, setBalance] = useState(null);

  const fetchBalance = async () => {
    try {
      const response = await axios.get("http://localhost:8080/api/company_accounts/balance");
      setBalance(response.data); // axios puts backend response in .data
    } catch (error) {
      console.error("Error fetching balance:", error);
    }
  };
