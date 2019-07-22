*Journal*
Rasmus Groth
*20181222, Utterslev, Copenhagen, Denmark*

# Upgrade all pip installed packages
pip install -U $(pip freeze | awk '{split($0, a, "=="); print a[1]}')
