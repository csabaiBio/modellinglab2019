**Project Assignment: Tight-Binding Modeling with sisl**

**Course:** Scientific Modelling Computer Lab  
**Tutor:** Zoltán Tajkov  

---

### **Project Title:** Exploring Tight-Binding Models of Layered Carbon Materials Using sisl

---

### **Objective:**
The goal of this project is to provide hands-on experience in tight-binding modeling of 2D and layered solids using the Python library **sisl**. Students will:
1. Learn the basic principles of tight-binding modeling for 2D solids.
2. Develop skills to create and manipulate geometries and Hamiltonians in **sisl**.
3. Analyze electronic structures, density of states (DOS), and band structures of graphene and graphite.
4. Explore stacking configurations and the effect of varying parameters in layered materials.

---

### **Project Tasks:**

#### **Part 1: Basics of Tight-Binding Modeling**
- **Study Component**: Review the theory of tight-binding modeling for 2D solids. Understand the concepts of:
  - Create low-energy Hamiltonians for solids.
  - On-site and the hopping amplitudes.
  - Periodic boundary conditions.

#### **Part 2: Graphene Modeling**
- **Task 2.1**: Using the **sisl** package, create a graphene sheet with a bond length of 1.42 Å. Do not use `geom.graphene()`; instead, construct the lattice step by step to understand the basics of geometry creation in **sisl**.
- **Task 2.2**: Visualize the graphene geometry:
  - Plot a 5x5 tiling of the graphene sheet.
  - Highlight the unit cell and draw bonds between atoms.
- **Task 2.3**: Define the electronic structure of graphene using:
  - An orthogonal basis.
  - Unpolarized spin configuration.
  - On-site energies set to 0 eV and nearest-neighbor hopping amplitudes set to -2.7 eV.
- **Task 2.4**: Calculate and visualize:
  - The band structure of graphene.
  - The density of states (DOS).
  - The projected density of states for the sublattices (PDOS).

#### **Part 3: Layered Graphite Modeling**
- **Task 3.1**: Construct N-layer graphite samples for both ABA (Bernal) and ABC (Rhombohedral) stacking configurations.
  - Set the interlayer hopping amplitude to -0.27 eV.
- **Task 3.2**: Write a script to automate the generation of N-layer geometries for both stacking configurations.
- **Task 3.3**: Analyze and visualize the electronic properties:
  - Density of States (DOS).
  - Projected Density of States (PDOS) on the top and bottom layers.
  - Band structures.

#### **Optional Extensions:**
- **Task 4.1**: Implement a distance-dependent hopping amplitude for out-of-plane interactions and Investigate the effect of shifting the top layer in an ABA structure to form an ABABABC stacking. Analyze the resulting changes in DOS and band structure.
- **Task 4.2**: Implement layer-dependent on-site terms to simulate the doping effects of a substrate and explore its effects on the density of states

---

### **References:**
- [sisl Documentation](https://zerothi.github.io/sisl/)
- Relevant course materials and lecture notes on solid-state physics.
