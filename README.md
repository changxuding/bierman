Bierman
=======

This project is written as a supplement to Gerald J. Bierman's "Factorization
Methods for Discrete Sequential Estimation".  Selected algorithms are
illustrated in Matlab (actually developed with Octave).  The emphasis is
on illustrating the use of these algorithms for problems requiring
"linearization" along with the "extended" filtering method.

Estimation of a static state is first illustrated.  Range only trackers
are used to estimate the location of an object within a boxed volume.
Estimation of a dynamics state follows by tracking movement of a wiffle
ball within a room using the same range only trackers.

driver_01.m
```
Compares estimation of a static state using full batch, sequential batch,
stabilized Kalman, Potter mechanization, and U-D sequential methods.
```

driver_02.m
```
Performs speed comparisons of the stabilized Kalman, Potter
mechanization, and U-D sequential estimation methods.  Percent
containment is also output.
```

driver_02b.m
```
Performs speed comparisons of the stabilized the Kalman, U-D, and SRIF
methods.  Percent containment is also output.
```

driver_02b_bias.m
```
Adds bias to the measurement model and then performs comparisons between
the Schmidt Kalman as a baseline and various implementations of the SRIF.
```

driver_householder.m - detour
```
Compares  A WLS solution of the normal equations with one using
Householder triangularization and QR decomposition.
```

driver_lls_constrained.m - detour
```
Illustrates constrained LLS via Lagrange multipliers.
```


driver_lls_hhcurvefit.m - detour
```
Illustrates sequential estimation via Householder SRIF for a linear
problem.
```

driver_lls_qrcurvefit.m - detour
```
Illustrates sequential estimation via a QR SRIF for a linear problem.
```

driver_ut_sigma_vec.m - detour
```
Visualization of unscented transform sigma vectors given an estimate
and covariance.
```

driver_03.m
```
Estimation of a dynamic state - simple wiffle ball in a room trajectory

This driver script is the first of this series of examples illustrating
filtering of a dynamic scenario.  A simple drag free trajectory is created
along with simulated range observations (using range trackers from previous
examples) that are subject to only measurement noise.  No bias effects
have been added.  The goal is to implement a simple filter (observation model
and dynamic model) that outperforms the WLS method (observation model only).
```

driver_03b.m
```
Estimation of a dynamic state - simple wiffle ball in a room trajectory

Illustrates the use of a reference trajectory to produce estimate
covariance as a function of time using the U-D filter.
```

driver_03ut.m
```
EKF and UKF are compared.  See driver_05utsr.m.
```

driver_03utsr.m
```
EKF and square root UKF are compared.  See driver_05utsr.m.
```

driver_04.m
```
Adds drag to the truth model for driver_03 while leaving it out of the
filter model.  Illustrates divergence in the filter and how to fix it
with the inclusion of process noise.
```

driver_04b.m
```
The same scenario as driver_04.m where the truth model includes drag and
the filter model doesn't.  Here, the U-D and SRIF methods are compared
where both incorporate process noise to account for the unmodeled drag
effect.
```

driver_04b2.m
```
Illustrates the use of a reference trajectory to produce estimate
covariance as a function of time using the SRIF when process noise
is present in the filter model.
```

driver_04c.m
```
A hybrid version of the SRIF is implemented where QR factorization via
modified Gram-Schmidt (MGS) decomposition is used for the observation
updates while Householder reflections are used for the prediction.  The
U-D, SRIF, and hybrid SRIF methods are compared processing one
observation at a time.  The hybrid method is also run where observation
sets are processed in batches.
```

driver_04d.m
```
The stabilized Kalman form is revisited and compared to the U-D method
and hybrid SRIF.  The Kalman and U-D methods process one observation at
a time while the SRIF process measurement sets in batch mode.
```

driver_04ut.m
```
EKF and UKF are compared under conditions where process noise exists.
See driver_05utsr.m.
```

driver_04utsr.m
```
EKF and square root UKF are compared under conditions where process noise
exists.  See driver_05utsr.m.
```

driver_05.m
```
The stabilized Kalman, U-D, and hybrid SRIF are run with process noise
and process noise compensation along with biased tracker locations
that are not compensated for.
```

driver_05b.m
```
The SRIF method with bias compensation and Schmidt Kalman are
implemented and compared to the standard Kalman filter.
```

driver_05c.m
```
Illustrates the use of a reference trajectory to produce estimate
covariance as a function of time using the Schmidt Kalman filter
when process noise is present in the filter model and systemic error
is present in the observation model.
```

driver_05d.m
```
Illustrates the use of a reference trajectory to produce estimate
covariance as a function of time using the SRIF when process noise
is present in the filter model and systemic error is present in the
observation model.
```

driver_05ut.m
```
Both the SKF and UKF with an augmented state vector are compared
when both process noise and observation bias are present.  See driver_05utsr.m.
```

driver_05utsr.m
```
All of the unscented Kalman filter examples have references this example.  It
compares the SKF, UKF, and square root UKF (SRUKF).  The unscented Kalman
really shines compared to other filters when observation model bias is present.
In fact, the author would argue most of the issues encountered with traditional
filtering problems that are passed off to being due to nonlinearities are, in
reality, due to observation bias not being properly accounted for.  If your
filter only includes process noise and you are OK with that, then you probably
don't fully understand what you are doing...

Therefore, this square root form, which should guarantee estimate covariance
stability, is the focus of the use of the unscented transform in this project.
This driver function and the square root form of the UKF will receive the most
use and best documentation.  While the square root form is computationally more
expensive than the standard UKF, the UKF is already significantly (order of
magnitude) slower than the EKF.  Therefore, if the benefits of the UKF are
desired, one might as well start with the full blown square root form.

This example includes observation model bias.  Compensating for observation
bias through the UT form of the Kalman filter requires augmenting the state
vector and associated covariance with consider parameters.  The observation
update step accounts for the influence of bias in both the state and covariance
update, but does not modify the consider parameters nor associated covariance.
This has been coined a Schmidt Kalman although it in no way resembles the
Schmidt Kalman that only considers the bias parameters.

The downside to this adding consider parameters to the state vector is a
significant increase in the computational burden for realistic filtering
problems.  The upside is the UKF digests observation bias much better than
the Schmidt Kalman and SRIF while reporting realistic estimate covariance.
If one can spare the extra CPU cycles, it is the way to go.
```

driver_05utsr_c.m
```
Illustrates covariance analysis given a reference trajectory for the (SR)UKF
method.  Also, focuses on the (SR)UKF vs. other UT examples.  Since only
the UT form of the Kalman was used for this example, different notation was
used for the driver script, that is more consistent with papers on the
topic of the (SR)UKF method.
```
