# tamrin_jalase7
import random
# تعریف کلاس ماشین
class Car:
    def __init__(self, id, color, fuel_capacity, max_speed, acceleration, brake_acceleration, fuel_efficiency, initial_fuel, fuel_consumption_rate):
        self.id = id
        self.color = color
        self.fuel_capacity = fuel_capacity
        self.max_speed = max_speed
        self.acceleration = acceleration
        self.brake_acceleration = brake_acceleration
        self.fuel_efficiency = fuel_efficiency
        self.initial_fuel = initial_fuel
        self.fuel_consumption_rate = fuel_consumption_rate
        self.current_fuel = initial_fuel
        self.distance_covered = 0
    
    def start(self):
        print(f"ماشین {self.id} با رنگ {self.color} راه افتاد.")
    
    def drive(self, distance):
        fuel_needed = (distance / 100) * self.fuel_consumption_rate
        if self.current_fuel >= fuel_needed:
            self.distance_covered += distance
            self.current_fuel -= fuel_needed
            print(f"ماشین {self.id} {distance} کیلومتر رانندگی کرد.")
        else:
            print(f"ماشین {self.id} سوخت کافی ندارد برای رانندگی.")
    
    def stop(self):
        print(f"ماشین {self.id} متوقف شد.")
    
    def refuel(self, amount):
        if self.current_fuel + amount <= self.fuel_capacity:
            self.current_fuel += amount
            print(f"ماشین {self.id} به میزان {amount} لیتر بنزین زد.")
        else:
            print(f"ماشین {self.id} نمی‌تواند بیش از ظرفیت باک بنزین بزند.")

# شبیه‌سازی مسابقه
def simulate_race(num_cars, track_length, fuel_stations):
    cars = []
    for i in range(num_cars):
        color = random.choice(["قرمز", "آبی", "سبز", "زرد", "سیاه"])
        fuel_capacity = random.randint(30, 60)
        max_speed = random.randint(150, 250)
        acceleration = random.uniform(2, 5)
        brake_acceleration = random.uniform(5, 10)
        fuel_efficiency = random.uniform(0.1, 0.2)
        initial_fuel = random.randint(30, 50)
        fuel_consumption_rate = random.randint(8, 15)
        
        car = Car(i + 1, color, fuel_capacity, max_speed, acceleration, brake_acceleration, fuel_efficiency, initial_fuel, fuel_consumption_rate)
        cars.append(car)
    
    # شروع مسابقه
    for car in cars:
        car.start()
    
    # رانندگی ماشین‌ها
    for car in cars:
        distance_remaining = track_length
        for station in fuel_stations:
            if distance_remaining > station:
                print(f"ماشین {car.id} به پمپ بنزین در {station} کیلومتر رسید.")
                fuel_to_add = random.randint(5, 15)
                car.refuel(fuel_to_add)
                distance_remaining -= (station - (track_length - distance_remaining))
        
        # رانندگی تا خط پایان
        car.drive(distance_remaining)
        car.stop()

    # اعلام نتایج
    print("\nنتایج مسابقه:")
    cars_sorted = sorted(cars, key=lambda x: x.distance_covered, reverse=True)
    
    # اعلام برنده
    winner = cars_sorted[0]
    print(f"\nبرنده مسابقه ماشین {winner.id} با رنگ {winner.color} است که {winner.distance_covered} کیلومتر رانندگی کرده.")
    
    # نمایش نتایج سایر ماشین‌ها
    for car in cars_sorted:
        print(f"ماشین {car.id} با رنگ {car.color} به مسافت {car.distance_covered} کیلومتر رسید.")
        
if __name__ == "__main__":
    num_cars = 5  # تعداد ماشین‌ها
    track_length = 1000  # مسافت مسیر مسابقه
    fuel_stations = [300, 600, 900]  # فاصله پمپ بنزین‌ها از مبدا
    
    # اجرای شبیه‌سازی مسابقه
    simulate_race(num_cars, track_length, fuel_stations)
