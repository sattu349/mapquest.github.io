import { useState } from "react";
import { Map, NavigationControl } from "react-map-gl";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Tabs, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { motion } from "framer-motion";
import "mapbox-gl/dist/mapbox-gl.css";

export default function TravelApp() {
  const [search, setSearch] = useState("");

  return (
    <div className="flex flex-col h-screen bg-gray-900 text-white">
      {/* Header */}
      <header className="flex justify-between p-4 bg-gray-800">
        <h1 className="text-xl font-bold">TravelMapX</h1>
        <Button variant="outline">Sign In</Button>
      </header>

      {/* Main Layout */}
      <div className="grid grid-cols-3 h-full">
        {/* Sidebar */}
        <aside className="p-4 bg-gray-850 border-r border-gray-700">
          <Tabs defaultValue="discover">
            <TabsList className="flex justify-between">
              <TabsTrigger value="discover">Discover</TabsTrigger>
              <TabsTrigger value="itinerary">Itinerary</TabsTrigger>
              <TabsTrigger value="bookings">Bookings</TabsTrigger>
            </TabsList>
          </Tabs>
          <Input
            className="mt-4"
            placeholder="Search places..."
            value={search}
            onChange={(e) => setSearch(e.target.value)}
          />
        </aside>

        {/* Map Section */}
        <main className="relative col-span-2">
          <Map
            initialViewState={{ latitude: 40.7128, longitude: -74.006, zoom: 10 }}
            mapStyle="mapbox://styles/mapbox/dark-v10"
            mapboxAccessToken={process.env.NEXT_PUBLIC_MAPBOX_TOKEN}
            className="w-full h-full"
          >
            <NavigationControl position="top-right" />
          </Map>
        </main>
      </div>

      {/* Floating Action Button */}
      <motion.div
        className="fixed bottom-6 right-6 bg-blue-500 p-4 rounded-full shadow-lg cursor-pointer"
        whileHover={{ scale: 1.1 }}
      >
        +
      </motion.div>
    </div>
  );
}
