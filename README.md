HERE'S HOW IT LOOKS
https://github.com/user-attachments/assets/b649a8d5-d7ec-4c89-a636-9a6115421fb7
account-overview h2 {
  font-size: 1.4rem !important;
  font-weight: 500;
}
.transactions h2 {
  font-size: 1.4rem !important;
  font-weight: 500;
  color: black;
}
body {
  font-family: Arial, sans-serif;
  background: #eef0f1;
  margin: 0;
  padding: 0;
}
 
.app {
  min-height: 100vh;
  animation: fadeIn 0.6s ease-in-out;
  position: relative;
  overflow: hidden;
  background-color: white;
}
 
.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 110%;
  height: 110%;
  background-size: cover;
  animation: moveBackground 60s linear infinite;
  transform: scale(1.05);
  z-index: -3;
}
 
.background-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4);
  z-index: -2;
}
 
@keyframes moveBackground {
  0% { transform: translateX(0) scale(1.05); }
  50% { transform: translateX(-2%) scale(1.05); }
  100% { transform: translateX(0) scale(1.05); }
}
 
.header {
  background: linear-gradient(270deg, #005893, #00a94f);
  background-size: 200% 200%;
  animation: headerGradient 8s ease infinite;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 6px 20px;
  color: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);
  position: relative;
  z-index: 10;
  transition: background 0.3s ease;
}
 
.header:hover {
  background: linear-gradient(270deg, #00a94f, #0070ba);
}
 
@keyframes headerGradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
 
.header-left {
  display: flex;
  align-items: center;
  gap: 20px;
}
 
.logo {
  height: 50px;
  cursor: pointer;
  transition: transform 0.2s ease;
 
}
 
.logo:hover {
  transform: scale(1.08);
}
 
.banking-dropdown,
.country-dropdown,
.user-switcher {
  padding: 5px;
  border-radius: 4px;
  border: none;
}
 
.header-right {
  display: flex;
  align-items: center;
  gap: 10px;
}
 
.search-bar {
  padding: 5px;
  border-radius: 4px;
  border: none;
  width: 200px;
}
 
.profile {
  display: flex;
  align-items: center;
  gap: 8px;
}
 
.avatar {
  background-color: #0070ba;
  color: white;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  font-weight: bold;
  animation: pulse 2s infinite;
}
 
@keyframes pulse {
  0% { box-shadow: 0 0 0 0 rgba(0, 112, 186, 0.6); }
  70% { box-shadow: 0 0 0 8px rgba(0, 112, 186, 0); }
  100% { box-shadow: 0 0 0 0 rgba(0, 112, 186, 0); }
}
 
.username {
  font-size: 14px;
}
 
 
h2 { margin: 10px 0 6px 0; background: #f6f8fa;
   color: #0367aa; padding: 2px 8px;
    border-radius: 4px;
    display: inline-block;
    font-size: 0.5rem;
     font-weight: 100;
      font-family: 'Segoe UI', Arial, sans-serif;
       border: none;
       letter-spacing: 0.5px;
       text-transform: uppercase;
       box-shadow: 0 1px 3px rgba(0,112,186,0.06);
       transition: color 0.2s, background 0.2s;
      }
 
.account-overview,
.transactions {
  background: white;
  border-radius: 8px;
  padding: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
  max-width: 1300px;
  margin: 20px auto;
}
 
table {
  width: 100%;
  border-collapse: collapse;
  background: white;
  animation: fadeIn 0.6s ease-in-out;
  position: relative;
  z-index: 5;
}
 
th, td {
  padding: 12px;
  border: 1px solid #ddd;
  text-align: center;
 
}
 
th {
  padding-left: 25px !important;
}
 
th {
  background-color: #0070ba;
  color: white;
}
 
tbody tr:hover {
  background-color: rgba(0, 112, 186, 0.05);
  transition: background-color 0.2s ease-in-out;
}
 
button {
  padding: 6px 12px;
  border: none;
  background-color: #0070ba;
  color: white;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.2s, box-shadow 0.2s;
}
 
button:hover {
  background-color: #00a94f;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);
}
 
.top-bar {
  margin: 15px 0;
  display: flex;
  gap: 10px;
  align-items: center;
}
 
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(5px); }
  to { opacity: 1; transform: translateY(0); }
}
 
@media (max-width: 768px) {
  .header {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }
 
  .header-right {
    flex-wrap: wrap;
    gap: 5px;
  }
 
  .search-bar {
    width: 150px;
  }
 
  .top-bar {
    flex-direction: column;
    align-items: flex-start;
  }
}
 
