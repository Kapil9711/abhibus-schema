```javascript
import mongoose from "mongoose";

// User Schema
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: [true, "Please enter your username"],
    unique: true,
    minLength: [5, "Username should be more than 5 characters"],
  },
  gender: {
    type: String,
    required: [true, "Gender is required"],
  },
  age: {
    type: Number,
    required: [true, "Age is required"],
  },
  isVerified: {
    type: Boolean,
    default: false,
  },
  dob: {
    type: Date,
    required: true,
  },
  email: {
    type: String,
    required: [true, "Please enter your email"],
    unique: true,
    validate: [validator.isEmail, "Please provide a valid email"],
  },
  phone: {
    type: String,
  },
  password: {
    type: String,
    required: [true, "Please enter your password"],
    minLength: [8, "Password length should be more than 8 characters"],
    select: false,
  },
  admin: {
    type: Boolean,
    default: false,
    select: false,
  },
  resetPasswordToken: String,
  resetPasswordExpires: String,
});

// City Schema
const citySchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
  },
  state: {
    type: String,
    required: true,
  },
  lat: {
    type: Number,
  },
  lon: {
    type: Number,
  },
  stopPoints: [
    {
      title: {
        type: String,
        required: true,
      },
      directions: {
        type: String,
        required: true,
      },
      lat: {
        type: Number,
      },
      lon: {
        type: Number,
      },
    },
  ],
});

// Bus Schema
const busSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, "Bus name is required"],
  },
  price: {
    type: Number,
    required: [true, "Price is required"],
  },
  busType: {
    type: String,
    enum: ["Ac", "Sleeper", "No Ac", "Seater"],
    required: [true, "Bus Type is required"],
  },
  capacity: {
    type: Number,
    required: [true, "Capacity is required"],
  },
  TypeOfSeats: {
    type: String,
    enum: ["male", "female", "single", "double"],
    required: true,
  },
  Amenities: {
    type: String,
    enum: [
      "Seat belt",
      "Wi-fi",
      "child seating",
      "Recliners",
      "Power outlets",
      "Private entrance",
      "Emergency exit",
    ],
    default: "",
  },
  rating: {
    value: {
      type: Number,
      required: true,
    },
    totalRatings: {
      type: String,
      required: true,
    },
  },
  liveTracking: {
    type: Boolean,
    default: false,
  },
  lat: {
    type: Number,
  },
  long: {
    type: Number,
  },
  availableSeats: {
    type: Number,
    required: [true, "Available Seats are required"],
  },
  bookedSeats: {
    type: Number,
    required: [true, "Booked Seats are required"],
  },
  status: {
    type: String,
    default: "active",
  },
  partner: {
    type: String,
    required: [true, "Partner is required"],
  },
  licensePlate: {
    type: String,
    required: [true, "License no. is required"],
  },
});

// Trip Schema
const tripSchema = new mongoose.Schema({
  busId: {
    type: mongoose.Schema.ObjectId,
    ref: "busModel",
    required: [true, "BusId is required"],
  },
  route: {
    startLocation: {
      type: String,
      required: [true, "Start Location is required"],
    },
    endLocation: {
      type: String,
      required: [true, "End Location is required"],
    },
    stops: [
      {
        title: {
          type: String,
          required: [true, "Stop title is required"],
        },
        arrivalTime: {
          type: String,
          required: [true, "Arrival Time is required"],
        },
        departureTime: {
          type: String,
          required: [true, "Departure Time is required"],
        },
      },
    ],
  },
  arrivalTime: {
    type: String,
    required: [true, "Arrival Time is required"],
  },
  departureTime: {
    type: String,
    required: [true, "Departure Time is required"],
  },
  driverName: {
    type: String,
    required: [true, "Driver name is required"],
  },
  status: {
    type: String,
    required: [true, "Status is required"], // Status of the trip (scheduled, in-progress, completed, canceled)
  },
});

// Bookings Schema
const bookingSchema = new mongoose.Schema({
  tripId: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "tripModel",
    required: true,
  },
  busId: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "busModel",
    required: true,
  },
  user: {
    type: mongoose.Schema.ObjectId,
    ref: "userModel",
    required: [true, "User id is required"],
  },
  seatNumber: {
    type: String,
    required: [true, "Seat Number is required"],
  },
  price: {
    type: String,
    required: [true, "Booking Price is required"],
  },
  seats_booked: {
    type: Number,
    required: true,
  }, // Number of seats booked
  booking_time: {
    type: Date,
    required: true,
    default: Date.now,
  }, // Time of booking
  status: {
    type: String,
    required: true,
    default: "confirmed",
  }, // Status of the booking (e.g., confirmed, canceled)
});
```
