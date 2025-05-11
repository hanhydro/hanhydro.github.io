---
title: "On the nonlinear methods solving outer loop in COMSOL"
excerpt: "Short description of portfolio item number 2 <br/><img src='/images/2025-05-11.png'>"
collection: portfolio
---

### Overview

Modern versions of COMSOL offer several practical options for solving nonlinear multiphysics problems using the Fully Coupled solver. At the core, these methods aim to simplify a complex nonlinear system by solving a series of linear ones. You can choose from three variations of Newton’s method, Automatic, Constant, and Automatic, Highly Nonlinear. Each method handles convergence, memory usage, and stability a little differently, and choosing the right one can make a big difference.

The Automatic (Newton) method is a solid all-around choice. It dynamically adjusts how big a step to take at each iteration, which makes it both fast and fairly forgiving if your starting guess isn’t great. It's well-suited for most problems that aren't too extreme in their nonlinearity.

If you already have a good starting point—like results from a previous time step or load increment—then the Constant (Newton) option can speed things up. It skips the extra calculations needed to adapt the step size and just uses the one you specify. The catch is that it’s less forgiving: if the step size is too large for the first few iterations, the solver might fail to converge.

For very tough problems—like those involving phase changes, large deformations, or tight coupling between physics—there’s Automatic, Highly Nonlinear (Newton). This mode plays it safe by starting with extremely small steps and gradually increasing them as it gains confidence. It’s slower but much more robust in challenging scenarios.

All three of these Newton-based strategies share a key strength: once they’re close to the solution and the steps become larger, they converge very quickly.


### So… Which One Should You Use?

A good general rule is to start with Automatic (Newton). It’s balanced, fast, and works for most applications.

If that doesn’t converge or keeps making tiny steps without improvement, switch to Automatic, Highly Nonlinear (Newton)—especially if your physics are tricky.

If your model is enormous and pushing the limits of your RAM, or if you’re solving a loosely coupled system, Segregated might be the way to go.

And when you’ve got a high-quality initial guess and want raw speed, try Constant (Newton) with a damping factor you trust.


### A Few Tips for Smoother Solving

* Watch the damping factor. If it stays tiny for too long, that’s a clue something might be wrong with your setup or scaling.
* Keep an eye on residual plots. If the residual flatlines, try reducing the step size or updating the Jacobian more often.
* Use continuation wisely. Solving a simpler version of the problem first can give you a great starting guess.
* Boost Segregated with acceleration. Techniques like Anderson acceleration can make fixed-point loops converge much faster.

Understanding the strengths and quirks of these solver options will help you get better results faster, and make sure the numerical method doesn’t become the bottleneck in your modeling process.
