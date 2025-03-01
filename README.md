import React, { useState } from "react";
import { BrowserRouter as Router, Route, Routes, Link } from "react-router-dom";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";

const farmers = Array.from({ length: 20 }, (_, i) => ({
  name: `Farmer ${i + 1}`,
  location: `Village ${i + 1}`,
  produce: `Produce ${i + 1}`,
  contact: `+91 98765${i}432${i}`
}));

const markets = Array.from({ length: 20 }, (_, i) => ({
  name: `Market ${i + 1}`,
  location: `City ${i + 1}`,
  products: `Product ${i + 1}`,
  contact: `+91 87654${i}321${i}`
}));

const customers = Array.from({ length: 5 }, (_, i) => ({
  name: `Customer ${i + 1}`,
  orders: `Order ${i + 1}`,
  contact: `+91 76543${i}210${i}`
}));

const ProfileDetails = ({ profile, onClose }) => (
  <div className="fixed top-0 left-0 w-full h-full bg-gray-900 bg-opacity-50 flex justify-center items-center">
    <div className="bg-white p-6 rounded-lg shadow-lg">
      <h2 className="text-xl font-bold">{profile.name}</h2>
      <p>Location: {profile.location}</p>
      <p>{profile.produce || profile.products || profile.orders}</p>
      <p>Contact: {profile.contact}</p>
      <Button onClick={onClose} className="mt-4">Close</Button>
    </div>
  </div>
);

const Home = () => {
  const [selectedProfile, setSelectedProfile] = useState(null);

  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold text-center">🌾 Farmer Marketplace 🌾</h1>
      <div className="grid grid-cols-2 gap-4 mt-4">
        <Card className="p-4">
          <img src="https://source.unsplash.com/300x200/?farm,vegetables" alt="Farm Produce" className="w-full rounded-lg" />
          <CardContent>
            <p>Fresh Organic Tomatoes - $5/kg</p>
            <Button className="mt-2">View Details</Button>
          </CardContent>
        </Card>
        <Card className="p-4">
          <img src="https://source.unsplash.com/300x200/?fruits,market" alt="Farm Fruits" className="w-full rounded-lg" />
          <CardContent>
            <p>Juicy Apples - $3/kg</p>
            <Button className="mt-2">View Details</Button>
          </CardContent>
        </Card>
      </div>
      <div className="mt-6 p-4 bg-gray-100 rounded-lg">
        <h2 className="text-xl font-bold">👨‍🌾 Farmers Profiles</h2>
        {farmers.map((farmer, index) => (
          <p key={index}>{farmer.name} - {farmer.location} <Button onClick={() => setSelectedProfile(farmer)}>Info</Button></p>
        ))}
      </div>
      <div className="mt-6 p-4 bg-gray-100 rounded-lg">
        <h2 className="text-xl font-bold">🛒 Market Profiles</h2>
        {markets.map((market, index) => (
          <p key={index}>{market.name} - {market.location} <Button onClick={() => setSelectedProfile(market)}>Info</Button></p>
        ))}
      </div>
      <div className="mt-6 p-4 bg-gray-100 rounded-lg">
        <h2 className="text-xl font-bold">👤 Customer Details</h2>
        {customers.map((customer, index) => (
          <p key={index}>{customer.name} - {customer.orders} <Button onClick={() => setSelectedProfile(customer)}>Info</Button></p>
        ))}
      </div>
      {selectedProfile && <ProfileDetails profile={selectedProfile} onClose={() => setSelectedProfile(null)} />}
    </div>
  );
};

const Login = () => (
  <div className="p-4 flex flex-col items-center">
    <h1 className="text-xl font-bold">🔑 Login / Signup</h1>
    <Input placeholder="Email" className="mt-2 w-80" />
    <Input type="password" placeholder="Password" className="mt-2 w-80" />
    <Button className="mt-2 w-80">Login</Button>
  </div>
);

const OrderPlacement = () => (
  <div className="p-4 flex flex-col items-center">
    <h1 className="text-xl font-bold">🛒 Place Order</h1>
    <Input placeholder="Enter Quantity" className="mt-2 w-80" />
    <Button className="mt-2 w-80">Confirm Order</Button>
  </div>
);

const OrderTracking = () => (
  <div className="p-4 flex flex-col items-center">
    <h1 className="text-xl font-bold">📦 Order Tracking</h1>
    <p className="mt-2">Status: <strong>Pending → Confirmed → Delivered</strong></p>
  </div>
);

const App = () => (
  <Router>
    <nav className="p-4 flex gap-6 justify-center bg-green-500 text-white font-bold">
      <Link to="/">🏠 Home</Link>
      <Link to="/login">🔑 Login</Link>
      <Link to="/order">🛒 Place Order</Link>
      <Link to="/track">📦 Track Order</Link>
    </nav>
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/login" element={<Login />} />
      <Route path="/order" element={<OrderPlacement />} />
      <Route path="/track" element={<OrderTracking />} />
    </Routes>
  </Router>
);

export default App;
