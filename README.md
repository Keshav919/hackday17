# Accelerometer controls for Google Cardboard and Daydream!
In an effort to improve the quality of cheap VR, this was an attempt to map a user's physical motion into the VR world to give a viewer an extra degree of control.
The system has 3 parts:

# 1. Server
A basic Node server. Largely unimportant, except for the fact that pages had to be served in order to use the VR libraries.

# 2. VR
VR experience was put together using two tools: three.js and StereoEffect.js by mrdoob.

# 3. Accelerometer Controls
OrbitalControls provided some of the functionality needed (rotational acceleration). The rest was the bulk of the project - the application grabbed linear acceleration data from the accelerometer API.
The first 100 milliseconds are used as sampling data. The user is asked not to move, and all accelerometer readings are recorded.
This sampling data is used to distinguish between true user motion and noise. Data with z-scores exceeding 5 in modulus (absolute value) are considered user motion. This data is stored in a vector (I custom-built the vector library for general use a while back) and integrated twice.
The resulting displacement vector is used to update the user's position in the VR world.
