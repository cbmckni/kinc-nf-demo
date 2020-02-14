KINC-NF Demoes for Kubernetes
===

#### 1. Configure Environment

If needed, add Java 8 to alternatives:

`update-alternatives --install <link> <command> <real_path> <priority>`

ex: `update-alternatives --install /usr/bin/java java /usr/local/bin/java 80`

Switch to Java 8:

`sudo update-alternatives --config java`

Select the correct number to switch versions, then confirm that you are using the correct version:

```
user@ubuntu:~/Desktop/kinc-nf-demo$ java -version
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (build 1.8.0_242-8u242-b08-0ubuntu3~18.04-b08)
OpenJDK 64-Bit Server VM (build 25.242-b08, mixed mode)

```
It should be 1.8.XXX.

#### 2. Load Input to Kubernetes Cluster

Go to the `kinc-nf-demo` folder:

`cd <PATH>/kinc-nf-demo`

Select one of the demoes in the `demos` folder to run:

 - `yeast-cpu`: Running the Yeast GEM on CPU resources.
 - `cervix-gpu`: Running the Cervix GEM on GPU resources.

Load the input data onto the PVC:

`./kube-load.sh <PVC> <DEMO_FOLDER>`

#### 3. Deploy Workflow

Deploy KINC using `nextflow-kuberun`:

`nextflow kuberun systemsgenetics/kinc-nf -v <PVC> -c demos/<DEMO_FOLDER>/nextflow.config`

Wait until the workflow is finished running.

#### 4. Retreive and Visualize Gene Co-expression Network

Copy the output of KINC from the PVC to your VM:

`./kube-save.sh <PVC> <DEMO_FOLDER>-output`

Open Cytoscape. (Applications -> Other -> Cytoscape)

Go to your desktop and open a file browsing window, navigate to `<PATH>/kinc-nf-demo/<DEMO_FOLDER>-output/<INPUT_GEM>`.

Finally, drag the file `<INPUT_GEM>.net` from the file browser to Cytoscape!

The network should now be visualized! 
