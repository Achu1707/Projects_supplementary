![img0](https://github.com/Achu1707/Projects/assets/150841023/a3703df1-81c2-413f-b0ca-8c789d8081ec)
![img1](https://github.com/Achu1707/Projects/assets/150841023/011cfccd-82d6-4177-bd8d-c7e7c2deb828)
[img2](https://github.com/Achu1707/Projects_supplementary/blob/main/3.png)

<p><strong>Aim</strong></p>
<p>To simulate an incompressible-laminar-viscous flow through the backward facing step geometry</p>
<p><strong>Objective</strong></p>
<p>Based on the described physics of flow choose the appropriate solver and Perform a transient simulation.Simulate for two different cases and compare the results</p>
<p><strong>Case 1</strong>&nbsp;- Simulate the flow without using any grading factor (i.e., GF = 1)</p>
<p><strong>Case 2</strong>&nbsp;- Simulate the flow with grading factor of 0.2. The cells should be finer near the walls (includig the step wall).</p>
<p><strong>Mesh specification</strong></p>
<ol>
<li>Number of cells along the x direction (longer dimension) = 200</li>
<li>Number of cells along the longer&nbsp;y direction = 20;</li>
</ol>
<p><strong>Boundary condition specification</strong></p>
<p>The domain specifications are provided in the following figure.</p>

<p><strong>Desired output</strong></p>
<ul>
<li>Measure the velocity profile at 0.085 m from the inlet of the geometry for both case studies and compare. You can use the plot over line tool for this.</li>
<li>Explain why Grading/Growth factor is essential for meshing.</li>
</ul>
<p>&nbsp;</p>
<p><strong>Answer</strong></p>
<p>In the question it is clearly mentioned to simulate an<u> incompressible-laminar-viscous flow</u> through the backward facing step geometry where the simulation should be <u>transient</u>. So the suitable solver will be <strong>icoFoam</strong>. I selected this solver based on information given in the <a href="https://www.openfoam.com/documentation/user-guide/a-reference/a.1-standard-solvers" target="_blank" rel="noopener">Openfoam website</a> .</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid3_1700768053.png" alt="" width="873" height="60" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>Fig 1. Solver selection</em></p>
<p><strong>Procedure</strong></p>
<p>1) First we have to copy the necessary icoFoam folder(cavity) from tutorials to run folder. Openfoam doesn'tallow us to do the simulation in tutorial folder so we are copying it to run folder. The step by step&nbsp; procedure on how I did this was dispayed in the image below.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid0_1700160251.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 2. Terminal window (to copy tutorial files to run folder)</em></p>
<p>2) Here we copied the cavity folder from icofoam, renamed as cavity_test and pasted in run folder. Inside this, we can see 3 sub folders : 0, constant and system.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid1_1700160251.png" alt="" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>Fig 3. Terminal window (to open blockMeshDict)</em></p>
<p>4) Inside system folder there is text file called blockMeshDict. It can be opened using gedit command. This file contains geometry and mesh options of the blockmesh for a sample model. Here, I changed the geometry according to the question.</p>
<p>The backward facing step was divided into 5 blocks as shown below.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid2_1700160250.png" alt="" width="646" height="203" /></p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;<em> Fig 4. Block numbering</em></p>
<p>The following numbering system were assumed for providing the appropriate vertices values for geometry setup and boundary.<img src="file:///C:/Users/singu/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg" alt="A diagram of a triangle with lines

Description automatically generated with medium confidence" width="636" height="254" border="0" /></p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid3_1700160251.jpg" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 5. Vertices numbering for each blocks</em></p>
<p><em>Source:&nbsp; Image taken from text help for blockMesh in Content section</em></p>
<p><strong>Case 1 (Grading factor =1)</strong></p>
<p class="MsoNormal">blockMeshDict file</p>
<pre class="language-cpp"><code>/*--------------------------------*- C++ -*----------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  8
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
FoamFile
{
    version     2.0;
    format      ascii;
    class       dictionary;
    object      blockMeshDict;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

convertToMeters 0.01;

vertices
(
    (0 0 0)  //0
    (8 0 0)  //1
    (8 0.5 0)  //2
    (0 0.5 0)  //3
    (8 1 0)  //4
    (0 1 0) //5
    (20 1 0) //6
    (20 0.5 0)  //7
    (20 0 0)  //8
    (20 -1 0)  //9
    (8 -1 0)  //10

    (0 0 0.2)  //11
    (8 0 0.2)  //12
    (8 0.5 0.2)  //13
    (0 0.5 0.2)  //14
    (8 1 0.2)  //15
    (0 1 0.2)  //16
    (20 1 0.2)  //17
    (20 0.5 0.2)  //18
    (20 0 0.2)  //19
    (20 -1 0.2)  //20
    (8 -1 0.2)  //21
);


blocks
(
    hex (0 1 2 3 11 12 13 14)
    (200 20 1)
    simpleGrading (1 1 1)

    hex (3 2 4 5 14 13 15 16)
    (200 20 1)
    simpleGrading (1 1 1)

    hex (2 7 6 4 13 18 17 15)
    (200 20 1)
    simpleGrading (1 1 1)

    hex (1 8 7 2 12 19 18 13)
    (200 20 1)
    simpleGrading (1 1 1)

    hex (10 9 8 1 21 20 19 12)
    (200 20 1)
    simpleGrading (1 1 1)
);

edges
(
);

boundary
(
    inlet   
    {
        type patch;
        faces
        (
            (0 11 14 3)
            (3 14 16 5)
        );
    }
    outlet
    {
        type patch;
        faces
        (
            (7 6 17 18)
            (8 7 18 19)
            (9 8 19 20)
        );
    }
    upperWall
    {
        type wall;
        faces
        (
            (5 16 15 4)
            (4 15 17 6)
        );
    }
    lowerWall
    {
        type wall;
        faces
        (
            (0 1 12 11)
            (10 21 12 1)
            (10 9 20 21)
        );
    }
    frontAndBack
    {
        type empty;
        faces
        (
            (11 12 13 14)
            (14 13 15 16)
            (13 18 17 15)
            (12 19 18 13)
            (21 20 19 12)
            (0 3 2 1)
            (3 5 4 2)
            (2 4 6 7)
            (1 2 7 8)
            (10 1 8 9)
        );
    }
);

mergePatchPairs
(
);

// ************************************************************************* //
</code></pre>
<p>Explanation</p>
<ol>
<li>The words inside the /*...*/ are called as comments.</li>
<li>Next the class FoamFile is called as dictionary which contains key value pairs. Value is 2.0.</li>
<li>Here I was taking the dimensions in cm. So it was converted to metres with factor of 0.01.</li>
<li>In vertices, the position of each vertices in x ,y and z axis were given in order as in Fig 5. First the x and y values were assigned for z=0 then for z=0.2.</li>
<li>Then in blocks section, the hex(0 1 2 3 11 12 13 14) represents block 1 as in Fig 4. (200 20 1) represents the no.of mesh points in x,y and z axis respectively.Then the simpleGrading (1 1 1) represents grading factor of 1 in all axes (x,y and z).</li>
<li>Grading factor is defined as the ratio of size of end cell of the block to its starting cell, in any axis. Here the value 1 represents the size of each cell is uniform in the axis.</li>
<li>Next the boundaries were assigned, inlet, oulet, upperWall, lowerWall, front and Back.</li>
</ol>
<p>The numbering were assigned based on right hand thumb rule. The thumb represents the direction of normal to the each surface and the fingers denote the direction of order of each vertices of the block. It may be confusing whether the direction maybe clockwise or anticlockwise. So a convention was followed here which say, if you look the surface from outside the block, the direction is anti clockwise, if you look the surface from inside the block, the direction is clockwise.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid4_1700768053.png" alt="" width="1030" height="560" /></p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid5_1700768053.png" alt="" width="909" height="270" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 6. a) Numbering and direction selection for looking the surface for each boundaries. b) boundary specification</em></p>
<p>Control dict</p>
<p>After editing the blockMeshDict file, control dict file is opened which is in the same system folder. Here we can give start time, end time, deltaT (time step) etc. Here start time as 0, end time as 2 and delta T as 0.00001 were assumed. The deltaT was chosen such that the CFL number should be less than 1. deltaT was arbitararly chosen first and while running the solver ,we can check if it is okay or not. If the solver stops before the end time, we have to change the deltaT as CFL no. would have crossed 1.</p>
<p>&nbsp;</p>
<pre class="language-cpp"><code>/*--------------------------------*- C++ -*----------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  8
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
FoamFile
{
    version     2.0;
    format      ascii;
    class       dictionary;
    location    "system";
    object      controlDict;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

application     icoFoam;

startFrom       startTime;

startTime       0;

stopAt          endTime;

endTime         0.04;

deltaT          0.00001;

writeControl    timeStep;

writeInterval   20;

purgeWrite      0;

writeFormat     ascii;

writePrecision  6;

writeCompression off;

timeFormat      general;

timePrecision   6;

runTimeModifiable true;


// ************************************************************************* //</code></pre>
<p>Inlet pressure and velocity</p>
<p>cd.. was used to get back to cavity_test folder. Then 0 folder was selected. Inside it has two files :p(Pressure) and U (velocity).</p>
<p>1) First I opended p file. Then I gave the values as below,</p>
<p>&nbsp;</p>
<pre class="language-cpp"><code>/*--------------------------------*- C++ -*----------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  8
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
FoamFile
{
    version     2.0;
    format      ascii;
    class       volScalarField;
    object      p;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

dimensions      [0 2 -2 0 0 0 0];

internalField   uniform 0;

boundaryField
{
    inlet
    {
        type            zeroGradient;
    }

    outlet
    {
        type            fixedValue;
        value           uniform 0;
    }
    
    upperWall
    {
        type            zeroGradient;
    }
    
    lowerWall
    {
        type            zeroGradient;
    }

    frontAndBack
    {
        type            empty;
    }
}

// ************************************************************************* //
</code></pre>
<p>2) Then I opened U file and gave the values as below</p>
<pre class="language-cpp"><code>/*--------------------------------*- C++ -*----------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  8
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
FoamFile
{
    version     2.0;
    format      ascii;
    class       volVectorField;
    object      U;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

dimensions      [0 1 -1 0 0 0 0];

internalField   uniform (0 0 0);

boundaryField
{
    inlet
    {
        type            fixedValue;
        value           uniform (1 0 0);
    }
    
    outlet
    {
        type            zeroGradient;
    }
    
    upperWall
    {
        type            noSlip;
        value           uniform (0 0 0);
    }

    lowerWall
    {
        type            noSlip;
        value           uniform (0 0 0);
    }
    
    frontAndBack
    {
        type            empty;
    }
}

// ************************************************************************* //</code></pre>
<p>&nbsp;</p>
<p>The initial and boundary conditions were set up. After going back to cavity_test folder, blockMesh was typed to create the mesh.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/polymesh_1700232435.jpg" alt="" width="1219" height="629" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 7. Creating mesh</em></p>
<p>Then the mesh was checked if it was correct.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/checkMesh_1700232461.jpg" alt="" width="1206" height="596" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<em>&nbsp; Fig 8. Checking the mesh</em></p>
<p>&nbsp;Then paraFoam was typed in commandline to view the mesh. The mesh plot I got was,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/main5_1700232565.jpg" alt="" width="1387" height="203" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 9. Mesh of backward step (for mesh points (200 20 1))</em></p>
<p>&nbsp;The mesh didn't look uniform as the size of the some block differs. So I changed the grid point values in blockmeshDict file accordingly as given below,</p>
<pre class="language-cpp"><code>blocks
(
    hex (0 1 2 3 11 12 13 14)
    (160 10 1)
    simpleGrading (1 1 1)
   

    hex (3 2 4 5 14 13 15 16)
    (160 10 1)
    simpleGrading 
    (1 1 1)

    hex (2 7 6 4 13 18 17 15)
    (240 10 1)
    simpleGrading (1 1 1)

    hex (1 8 7 2 12 19 18 13)
    (240 10 1)
    simpleGrading (1 1 1)

    hex (10 9 8 1 21 20 19 12)
    (240 20 1)
    simpleGrading (1 1 1)
);</code></pre>
<p>&nbsp;Then the mesh was viewed in paraFoam.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid0_1700514220.png" alt="" width="1018" height="209" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 10. Mesh of backward step (for mesh points altered to get uniform mesh)</em></p>
<p>&nbsp;</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid1_1700514220.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 11. Mesh of backward step (zoomed view) (for mesh points altered to get uniform mesh)</em></p>
<p>Now the command icoFoam was run. When the solver reached the end time, it stopped. Now the paraFoam was used to visualize the plots.</p>
<p>In paraview, the play button was clicked to show how the velocity varies when time increases. The velocity plot at time 0.398 s was shown below,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid5_1700517245.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 12. Velocity distribution (case 1, GF=1)</em></p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid6_1700517245.png" alt="" width="946" height="400" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>Fig 13. Velocity distribution near the step (case 1, GF=1)</em></p>
<p>The pressure plot at time 0.4 s as shown below,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid7_1700517245.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 14. Pressure distribution</em></p>
<p>Go to Filters &rarr; Data Analysis &rarr; Plot over line to show the velocity distribution at 0.085 m from inlet.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid8_1700517245.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 15. a) Plot over line window</em></p>
<p>&nbsp;</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid0_1700761346.png" alt="" width="650" height="501" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<em> Fig 15. b) Velocity profile at 0.085 m from inlet at t=0 upto t=0.02s</em></p>
<p><strong>Case 2 (With grading factor 0.2)</strong></p>
<p>After applying the grading factor of 0.2 (for region near the walls) in the blockMeshDict file,</p>
<pre class="language-cpp"><code>blocks
(
    hex (0 1 2 3 11 12 13 14)
    (160 10 1)
    simpleGrading 
    (0.2 8 1)  

    hex (3 2 4 5 14 13 15 16)
    (160 10 1)
    simpleGrading 
    (0.2 0.2 1)

    hex (2 7 6 4 13 18 17 15)
    (240 10 1)
    simpleGrading (8 0.2 1)

    hex (1 8 7 2 12 19 18 13)
    (240 10 1)
    simpleGrading (8 8 1)
    
    hex (10 9 8 1 21 20 19 12)
    (240 20 1)
    simpleGrading (8 0.2 1)
);</code></pre>
<p>After saving the blockmeshdict file, the blockmesh and checkmesh command were run and visualised the mesh in paraview,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid10_1700526314.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 16. Mesh of backward step (with grading factor 0.2)</em></p>
<p>The zoom view.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid11_1700526314.png" alt="" width="1017" height="342" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 17. Mesh of backward step with fine mesh near the step (Zoomed view)<br /></em></p>
<p>Then in command window,icoFoam was run. When the solver reached the end time, it stopped. Now the paraFoam was used to visualize the plots.In paraview, the play button was clicked to show how the velocity varies when time increases. The velocity plot at time 0.4 s was shown below,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid17_1700528973.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 18. Velocity distribution (case 2, GF=0.2)</em></p>
<p>The velocity distribution near the step,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid18_1700528974.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 19. Velocity distribution near the step (case 2, GF=0.2)</em></p>
<p>The pressure plot,</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid19_1700528974.png" alt="" /></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 20. Pressure distribution (case 2, GF=0.2)</em></p>
<p>The velocity profile at 0.085 m from inlet.</p>
<p><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid1_1700761347.png" alt="" /></p>
<p><em>&nbsp;Fig 21. b) Velocity profile at 0.085 m from inlet at t=0 upto t=0.02s (Case 2 GF=0.2)<br /></em></p>
<p><strong>Results</strong></p>
<p>Comparison of velocity plot for case 1 and 2</p>
<p><strong>Case 1 (GF =1)<br /></strong></p>
<p><strong><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid16_1700526314.png" alt="" /></strong></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 22. Velocity distribution with uniform mesh (case 1, GF=1)</em></p>
<p>Here we can clearly see that the velocity didn't change much near the step, after 0.085 m it gradually decreases. The mesh is uniform and smooth here. The velocity also undergoes gradual change.</p>
<p><strong>Case 2(GF=0.2)</strong></p>
<p><strong><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid21_1700528974.png" alt="" width="923" height="425" /></strong></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 23. Velocity distribution (case 2, GF=0.2)</em></p>
<p>&nbsp;Here, we can clearly see that the mesh is finer near the step wall. The velocity changes very well near the step and decreases further as length increases.</p>
<p><strong>Velocity profile comparison at 0.085 m from inlet</strong></p>
<p><strong><img src="https://d3ocdjih6hdmey.cloudfront.net/lms-ci3/challenge/assets/2023/11/blobid2_1700761347.png" alt="" /></strong></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 24. Velocity profile comparison for case 1 and 2 at 0.085 m from inlet</em></p>
<p>In this plot, in case 1 we can see that the velocity increases exponentially hits the peak value and decreases gradually. The peak value of velocity is 1.1 m/s (around 0.014 s) at 0.085 m which is larger the the inlet velocity (1m/s).</p>
<p>In case 2, the peak value is 0.76 m/s (around 0.0102 s) which is smaller than the inlet velocity (1m/s).</p>
<p><strong>Conclusion</strong></p>
<p>In case 1 ,the mesh and velocity distribution seems smooth and it may be pleasing to us that it is the accurate solution. But it is not. When ever the geometry of the block changes (if there is a step) the flow velocity is going to change anyway. In order to capture the velocity change at the step, it is necessary to have more mesh points (finer mesh) so as to capture more of the velocity changes accurately and that we can get the result which may be close to experimental result. In case 2, the mesh near the step is made finer so it captures more of velocity change (Due to finer and more mesh points) and its distribution than in case 1.&nbsp;</p>
<p>Therefore the use of grading factor (G.F=0.2 in case 2) to have the finer mesh near the step wall is necessary to get the accurate results.</p>
