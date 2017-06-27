# Linked Data Platform for Animal Breeding & Genomics

This software provides semantically integrated genotypic/phenotypic data on animals to enable ranking of candidate genes associated with traits of interest (e.g. nipple quantity in pig).

**1. Clone this git repo.**

```
git clone --recursive https://github.com/candYgene/abg-ld.git
cd abg-ld
```

**2. Pull pre-built Docker image with [Virtuoso Universal Server](http://virtuoso.openlinksw.com/) from the [Docker Hub](https://hub.docker.com) registry.**

`docker pull candygene/docker-virtuoso`

Alternatively, you can build the image locally.

`docker build -t candygene/docker-virtuoso docker-virtuoso`

**3. Start the Virtuoso server.**

```
cd src
docker run --name abg-ld -v $PWD:/tmp/share -p 8890:8890 -d candygene/docker-virtuoso
```

**4. Prepare & ingest RDF data.**

```
tar xvzf ../data/pigQTLdb-ld.tar.gz -C ../data
mv ../data/rdf/* .
docker exec abg-ld make all # check virtuoso.log for potential errors
```
(other `make` rules: `install-pkgs`, `import-rdf`, `update-rdf`, `post-install`, `clean`)

**5. [Login](http://localhost:8890/conductor) to running Virtuoso instance for admin tasks.**

Use `dba` for both account name and password.

**6. Run queries via Virtuoso [SPARQL endpoint](http://localhost:8890/sparql) or browse data via [Faceted Browser](http://localhost:8890/fct/) (no login required).**

RDF graphs:IRIs (_A-Box_)
  * Pig QTLdb: `http://www.animalgenome.org/QTLdb/pig`
  * Ensembl: `http://www.ensembl.org/pig`, `http://www.ensembl.org/human`
  * UniProt: `http://www.uniprot.org/proteomes/pig`
  * OMIM: `http://bio2rdf.org/omim_resource:bio2rdf.dataset.omim.R4`

RDF graphs:IRIs (_T-Box_)
  * FALDO: `http://biohackathon.org/resource/faldo.rdf`
  * SO[FA]: `http://purl.obolibrary.org/obo/so.owl`
  * SIO: `http://semanticscience.org/ontology/sio.owl`
  * RO: `http://purl.obolibrary.org/obo/ro.owl`
  * VT: `http://purl.obolibrary.org/obo/vt.owl`
  * CMO: `http://purl.obolibrary.org/obo/cmo.owl`
  * LPT: `http://purl.bioontology.org/ontology/LPT`
  * LBO: `http://purl.bioontology.org/ontology/LBO`
  * Uniprot Core: `http://purl.uniprot.org/core/`

Further details can be found on the [wiki](https://github.com/candYgene/abg-ld/wiki/Home).
