import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Mic, Send, ShoppingCart, CheckCircle, XCircle } from "lucide-react";

export default function AgriLinkChatOrders() {
  const [messages, setMessages] = useState([]);
  const [orderStatus, setOrderStatus] = useState("Pending");
  const [inputMessage, setInputMessage] = useState("");
  const [deliveryStatus, setDeliveryStatus] = useState("Not Dispatched");

  const sendMessage = () => {
    if (!inputMessage.trim()) return;
    setMessages([...messages, { text: inputMessage, sender: "You" }]);
    setInputMessage("");
  };

  const placeOrder = () => {
    setOrderStatus("Order Placed");
  };

  const acceptOrder = () => {
    setOrderStatus("Accepted");
  };

  const rejectOrder = () => {
    setOrderStatus("Rejected");
  };

  const dispatchOrder = () => {
    setDeliveryStatus("Dispatched");
  };

  const completeOrder = () => {
    setDeliveryStatus("Delivered");
  };

  return (
    <div className="p-6 max-w-2xl mx-auto space-y-4">
      <Card>
        <CardContent className="p-4 space-y-2">
          <h2 className="text-xl font-bold">💬 Direct Messaging</h2>
          <div className="h-40 overflow-y-auto border p-2 rounded bg-gray-100">
            {messages.map((msg, index) => (
              <div key={index} className="mb-1">
                <strong>{msg.sender}: </strong>
                <span>{msg.text}</span>
              </div>
            ))}
          </div>
          <div className="flex space-x-2">
            <Textarea
              value={inputMessage}
              onChange={(e) => setInputMessage(e.target.value)}
              placeholder="Type your message..."
            />
            <Button onClick={sendMessage} className="flex items-center">
              <Send className="w-4 h-4 mr-1" /> Send
            </Button>
            <Button variant="outline" className="flex items-center">
              <Mic className="w-4 h-4 mr-1" /> Voice
            </Button>
          </div>
        </CardContent>
      </Card>

      <Card>
        <CardContent className="p-4 space-y-2">
          <h2 className="text-xl font-bold">📦 Order Placement & Tracking</h2>
          <p className="text-lg">Order Status: <span className="font-semibold">{orderStatus}</span></p>
          <p className="text-lg">Delivery Status: <span className="font-semibold">{deliveryStatus}</span></p>
          <div className="space-x-2">
            <Button onClick={placeOrder} className="flex items-center">
              <ShoppingCart className="w-4 h-4 mr-1" /> Place Order
            </Button>
            <Button onClick={acceptOrder} variant="success">
              <CheckCircle className="w-4 h-4 mr-1" /> Accept Order
            </Button>
            <Button onClick={rejectOrder} variant="destructive">
              <XCircle className="w-4 h-4 mr-1" /> Reject Order
            </Button>
            <Button onClick={dispatchOrder} variant="secondary">
              🚚 Dispatch Order
            </Button>
            <Button onClick={completeOrder} variant="success">
              ✅ Mark as Delivered
            </Button>
          </div>
        </CardContent>
      </Card>
    </div>
  );
}
