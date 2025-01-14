<h1 align="center"> FEniCSx scripts for MEALOR II Summer School </h1>
<h2 align="center"> Summer school website: https://mealor2.sciencesconf.org </h2>
<p align="center">
  <img src="https://mealor2.sciencesconf.org/data/pages/montage1.png" />
</p>

## Preamble

For the numerical sessions of MEALOR II, we will work with Jupyter notebooks and Python scripts.

The contents rely on various open-source projects:
* [FEniCSx](https://fenicsproject.org/) for the finite-element analysis (`dolfinx` >= 0.6). For a short introduction of FEniCSx in solid mechanics, [see the following tutorials](https://gitlab.enpc.fr/navier-fenics/fenicsx-tutorials)
* [Gmsh](https://gmsh.info/) Python API for the mesh generation
* [MFront](https://tfel.sourceforge.net/) for complex material constitutive modeling (`TFEL` >= 4.1) along with:
   - the [MFrontGenericInterfaceSupport](https://github.com/thelfer/MFrontGenericInterfaceSupport) project (`MGIS` >= 2.1)
   - the [dolfinx_materials](https://gitlab.enpc.fr/navier-fenics/dolfinx_materials) package for interfacing MFront with FEniCS.

We will also make a small use of [pyvista](https://pyvista.org/) for some plotting. However, most visualization of results will be done using [Paraview](https://www.paraview.org/).

To avoid cumbersome installation procedures, we provide a self-contained Docker image which you need to download, see installation instructions below. You only need to download and install Paraview on your machine for the visualization.

## Installation instructions

0. Install Paraview on your system : https://www.paraview.org/download/
   
2. Install Docker on your system : https://docs.docker.com/desktop/. For Linux users, make sure to add your username to the Docker user group (cf. [Linux post-installation steps for Docker Engine](https://docs.docker.com/engine/install/linux-postinstall/))

3. Once Docker is installed and running (you may need to reboot first), open a terminal and run the following commands

- 2.1 First, clone the MEALOR project repository:
  
  ```bash
  git clone https://github.com/MEALORII/TP_MEALOR.git
  ```

  If you don't have `git` installed, [download directly the source files](https://github.com/MEALORII/TP_MEALOR/archive/refs/heads/main.zip), extract them and navigate to the corresponding folder from the terminal.

- 2.2 Then pull the Docker image by running in the same terminal (this may take a while, approx 5 Go to download):

    ```bash
    docker pull ghcr.io/bleyerj/mealor:latest
    ```
 
 - 2.3 Then run the image with either:  

     * on **Mac/Linux**:
  
      ```bash
      docker run --init --rm -ti -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -e CHOWN_HOME=yes -e CHOWN_EXTRAOPTS='-hR' --user root -v "$(pwd)":/home/jovyan/shared ghcr.io/bleyerj/mealor:latest
      ```
      or, equivalently,
      ```bash
      sh TP_MEALOR/launch_mealor.sh
      ```
     
    * on **Windows**:
    
    ```bash
    docker run --init --rm -ti -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -e CHOWN_HOME=yes -e CHOWN_EXTRAOPTS='-hR' --user root -v "%cd%":/home/jovyan/shared ghcr.io/bleyerj/mealor:latest
    ```
    

3. Then you should see something like:
    ```
    To access the server, open this file in a browser:
     file:///home/jovyan/.local/share/jupyter/runtime/jpserver-369-open.html
     Or copy and paste one of these URLs:
     http://6af88686bce5:8888/lab?token=b955811ee149cada75db27258e6889a9cbee18a8afaeb373
     or http://127.0.0.1:8888/lab?token=b955811ee149cada75db27258e6889a9cbee18a8afaeb373
    ```
    Click on one of the links or copy and paste into your Web browser

4. A JupyterLab instance should now open.
   
   Navigate into the `TP_MEALOR` folder.

   Inside JupyterLab open a terminal and run
   ```
   pip install mealor/ --user
   ```

6. You can now open any of the notebooks and start working.

Your results will be saved into ".xdmf" file formats that you can open with Paraview for visualization

**Test installation**: Run the notebook [Test_Installation.ipynb](Test_Installation.ipynb) to check that everything is properly installed.

**Reuse**: For later usage, just start at step 2.3.
