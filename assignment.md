<h1 style="text-align:center">Lens Modeling</h1>
<p style="text-align:center"><i>Project created by Dr. Simon Birrer at Stony Brook University</i></p>
<br>

<hr>

<h2>Objective</h2>

This project aims to:

- Help you familiarize yourself with astronomical imaging data products;
- Teach you how to reconstruct the lensing distortions from a given observed image;
- Perform posterior inference for meaningful statistical interpretations.

The project is a derivative of the [lens modeling tutorial](https://github.com/ajshajib/lens_modeling_tutorial) by A. Shajib.

The final product of this project is a Jupyter notebook presenting the modeling of a real lens observed by the Hubble Space Telescope.

<h2>Modeling a Mock Lens</h2>

- [ ]  Check out the notebook [*Fitting a Lens Model by Hand*](https://github.com/ajshajib/lens_modeling_tutorial/blob/main/notebooks/Fitting%20a%20lens%20model%20by%20hand.ipynb) and try to develop an intuition for how different parameters involved in a lensing system can change the look of the system.
    - [ ]  Create a perfectly round Einstein ring by appropriately choosing the slider values in the section *Simulating a Lens System*.
    - [ ]  In the section *Demonstration of Lens Modeling by Tuning Parameters by Hand*, try to achieve a reduced $\chi^2$ as close to 1 as possible. If you want to look at the right answers, they’re given here.
- [ ]  Work with the notebook [*Intro to Lens Modeling with Lenstornomy.*](https://github.com/ajshajib/lens_modeling_tutorial/blob/main/notebooks/Intro%20to%20lens%20modeling%20with%20lenstronomy.ipynb) Fit the lensing system given to you. The fitting is done well when you get a reduced $\chi^2$ very close to 1.
- [ ]  Understand everything that is being done in the notebook. (It’s fine to not fully understand `kwargs_likelihood` and `kwargs_numerics` at this point.)
- [ ]  Run an MCMC after the PSO (Particle Swarm Optimization). Ensure that the MCMC chain has converged. Obtain the best-fit values and uncertainties for $\theta_E$ and $\gamma$.

<h2>Modeling a Real Hubble Space Telescope Image</h2>

- [ ]  Read the paper by [Rafee et al](https://ui.adsabs.harvard.edu/abs/2024arXiv241200361R/abstract).
- [ ]  Pick one lens from the [BDLensing repository](https://github.com/AstroBridge/BDLensing/tree/main/lens_systems) that was modeled by Rafee et al.
- [ ]  Get the lens imaging data in `.h5` format. Also, get the `psf.h5` file from this same folder. You have to model the lens system with `lenstronomy` in a Jupyter notebook (following the structure of *Intro to Lens Modeling with Lenstronomy*). The notebook must show the model decomposition plots as in the *Intro to Lens Modeling with Lenstronomy* notebook. Your notebook may only run PSO and running MCMC is not required.

Now, here are some directions for you to do the lens modeling.

- [ ]  State your name and the people you got help from for this assignment at the top of the notebook in a Markdown cell.
- [ ]  Check the notebook *Loading Data from `h5` Files* to see how to read the HDF5 files.
- [ ]  Make sure the appropriate PSF is being provided to `lenstronomy` through `kwargs_psf`.
- [ ]  You need to add external shear to the `lens_model_list` with the profile name `SHEAR`. The free parameters in this profile are: `gamma1` and `gamma2`, and the fixed parameters are `ra_0: 0`, `dec_0: 0`. The upper and lower values for `gamma1` and `gamma2` are 0.3 and -0.3. (`lenstronomy` [documentation](https://lenstronomy.readthedocs.io/en/latest/lenstronomy.LensModel.Profiles.html#lenstronomy.LensModel.Profiles.shear.Shear)).
- [ ]  You need to add the `SHAPELETS` light profile to the `source_model_list`. The free parameters are `beta`, `center_x`, and `center_y`. But, `center_x` and `center_y` need to be joined with the `center_x` and `center_y` of the Sersic light profile in the `source_model_list`. The fixed parameter is `n_max`, you can try values between 4 and 6 for the fixed value of `n_max`. (`lenstronomy` [documentation](https://lenstronomy.readthedocs.io/en/latest/lenstronomy.LightModel.Profiles.html#module-lenstronomy.LightModel.Profiles.shapelets))

If useful, you may try to get help from this tutorial notebook on lens modeling with `lenstronomy`: [Modeling a Simple Einstein Ring](https://github.com/lenstronomy/lenstronomy-tutorials/blob/main/Notebooks/LensModeling/modeling_a_simple_Einstein_ring.ipynb).

- [ ]  Try to modify the existing notebook on the BDLensing repository. What choices can be made differently? Will this affect the lens model inference?
- [ ]  Discuss how similar/different your lens model is compared to [Rafee et al.](https://ui.adsabs.harvard.edu/abs/2024arXiv241200361R/abstract)