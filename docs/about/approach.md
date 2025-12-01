# Technical Approach

## Why the Material Point Method?

Solid mechanics-based numerical analysis in the offshore renewable energy industry, and engineering in general, is dominated by the Finite Element Method (FEM). However, the FEM struggles to analyze problems involving very large deformation due to issues associated with:

- Mesh distortion
- Remeshing requirements
- Remapping of state variables (such as parameters for the history-dependent nature of soil)

### Alternative Methods and Their Limitations

Several alternative numerical methods exist, each with distinct advantages and limitations:

#### Coupled Eulerian-Lagrangian Method (CELM)

The CELM avoids many of the FEM's difficulties and is the primary numerical method that has been used to model large deformation problems to date, mainly due to its availability in commercial software (Abaqus). However:

- Requires fine meshes (high computational cost and time)
- Struggles with boundary conditions and tracking of free surfaces
- Has not achieved widespread use in the ORE industry

#### Particle Finite Element Method (PFEM)

The PFEM relies on continuous and extensive remeshing, but:

- Is computationally expensive
- Unproven for 3D ORE problems
- Not available commercially

#### Discrete Element Method (DEM)

The DEM has been adopted by industry for some soil-structure interaction problems due to the availability of commercial and open source software (PFC, Yade, LAMMPS, etc.). However:

- Issues exist in calibrating suitable particle interaction models to represent bulk material behaviour
- Analyses are very expensive compared to continuum-based approaches

### MPM Advantages

**The Material Point Method (MPM) overcomes the FEM/CELM/PFEM/DEM issues** and has been demonstrated by researchers at Durham University to be viable for ORE industry-relevant, large deformation soil-structure interaction problems.

We believe that the MPM is the ideal approach to tackle the large deformation soil-structure interaction problems faced by the ORE community.

## Building on Previous Work

Through existing EPSRC support, Durham University has developed the AMPLE code—an implicit implementation of the MPM designed to help people understand and use the method for problems ranging from small demonstrations to large-scale simulations.

### Key Features of Durham's MPM Implementation

**Implicit Formulation**: As with all of Durham's MPM research, the governing equations controlling the physical response are solved implicitly. This is in contrast to most other open source codes, which are restricted to explicit analysis. These explicit implementations have performance limitations when solving coupled (soil-water) interaction problems due to the CFL condition severely constraining the maximum time step size.

**Julia Language**: The code has been implemented in the high-performance Julia programming language (julialang.org). Julia was selected as it provides a good balance between performance and readability, which allows accessible code to be written that is:

- Easy to understand
- Easy to use and extend
- Deployable (reproducible coding environments)
- Efficient across different operating systems and high-performance computing (HPC) hardware

**Soil-Structure Interaction**: The existing implementation already includes soil-structure interaction for coupled problems, providing the core base for this proposal.

### The Transformation Challenge

The key progression offered by this project is making this academic, command-line accessed software accessible to engineers working in the ORE sector **without a low-level coding requirement**.

The approach to transforming this academic software into an open source software environment will be informed by successful examples, such as:

- Cuclix
- Firedrake
- FreeFEM
- OpenFOAM
- OpenSees
- OpenSCAD

## Work Packages

The project has four Work Packages (WPs) designed to deliver a maintainable, useable, and industry-ready software tool.

### WP1: Maintainable and Sustainable Base Code Environment

This WP focuses on setting up an appropriate platform for long-term software sustainability. The developed software will be open access under a GPL License, allowing other users to develop new software features and capabilities beyond this project's scope.

**Key Activities:**

- Automated building of the code (including support for diverse physical hardware and operating software environments)
- Version control via GitHub
- Automated documentation (on GitHub pages) via structured commented code
- Bug tracking and fixing
- Automatic testing (including automated monitoring and alerting of issues using native Julia tools)
- Addition of new features

The code will be developed within the framework of **Continuous Integration/Continuous Deployment (CI/CD)**, which will automatically build, test, and deploy base code changes when pushed to the GitHub repository.

**Deliverables:**

- Maintainable base code
- Article in Advances in Engineering Software

### WP2: Software Scoping Through User Engagement

End users' needs are core to the developed software. This WP focuses on scoping requirements through focused online workshops with participants from supporting offshore geotechnical stakeholders.

**Focus Areas:**

- Front-end interaction with the core code engine
- Scripting and batching of problem realizations
- Results visualization and output formats
- Exemplar problems that should be included as demonstration cases
- Required material models for soil behaviour
- Requirements categorization based on user type (geotechnical engineering consultant versus in-house software engineer)

Workshops will be summarized into briefing notes distilling key recommendations and proposed solutions/workflows, circulated for comment, prioritization, and approval prior to development. A feedback loop will be defined, allowing stakeholders to report on software interactions beyond the scoping workshops.

**Deliverables:**

- Software briefing/scoping notes
- Prioritization of tasks/features

### WP3: Software Interaction

This WP is split into three components:

#### Front-End Development

- Define workflow for running an analysis
- Facilitate the use of general material models for soil behaviour
- Provide 2D and 3D example test cases for problems such as:
  - Cone Penetration Tests (CPTs)
  - Spudcan penetration and extraction
  - Foundation installation
  - Cable ploughing
  - Anchor penetration

**Python** will be adopted as the industry-standard language for analysis scripting as a high-level software front end. The **STL file format** will be used to define rigid bodies interacting with deformable soil. Additional material constitutive models will be included via the widely used **Abaqus UMAT file format**.

#### Code Deployment

Focused on making deployment as straightforward as possible across various operating systems and computational hardware, including local and cloud-based implementations.

#### Outputs and Visualization

- Define workflow for visualizing analysis results
- Set output file formats
- Define methods allowing users to specify specific output information (such as force components on specific parts of a rigid body)

Output visualization will be facilitated by existing open source post-processing software, specifically **ParaView** and **VisIt**.

**Deliverables:**

- Clear workflow for setting up, running, and visualizing analyses
- Test cases
- UMAT interface
- Installation guides
- Deployment packages

### WP4: Training and Learning Resources

This WP provides learning resources and training to facilitate use of the developed software. Resources will be provided for users to understand both the fundamental methods/techniques and how to use the software to conduct engineering analysis.

**Learning Resources:**

- Core software documentation
- Test cases
- Video tutorials on model setup, running, and post-processing
- Recorded lectures on fundamentals of the MPM
- Videos explaining the core software

Towards the end of the project, two 2-day training workshops (one in-person, one online) will be provided free to members of the ORE geotechnical community.

**Deliverables:**

- Comprehensive learning resources
- Training workshops

## Research Environment

The Department of Engineering at Durham University is the ideal place from which to deliver this project. **Computational Mechanics** is one of the Department's strategic areas of research excellence (one of eight Research Nodes). It includes nine members of academic staff with broad, complementary experience of numerical methods applied to solving engineering problems.

The project is also supported by Durham University's **Advanced Research Computing (ARC)** team, which provides:

- Professional-level development practices and software engineering expertise
- Continuous Integration and Deployment (CI/CD) experience
- Test-driven development expertise
- Understanding and experience of large-scale open source software projects
- Software project management proficiency

## Risk Management

### Technical Risk Mitigation

All fundamental research objectives have already been achieved via previous EPSRC-funded projects. Technical risks are mitigated by:

- The experience of Durham's ARC team supporting the project
- Proven track record with the MPM approach
- Existing validated and benchmarked implementation

### Software Adoption Risk Mitigation

Software adoption risk is mitigated by stakeholder involvement from project inception to final delivery, ensuring the developed tool meets real industry needs.

### Recruitment Risk Mitigation

Recruitment of suitable staff is mitigated by the named researcher on the proposal who developed the current MPM Julia code and is therefore ideally placed to deliver the proposed project.
