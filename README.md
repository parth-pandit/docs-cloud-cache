# docs-cloud-cache

## About Branches 

On 7/7/17, **v1.0-branch** is your branch for (already released) v1.0. **v1.1 branch** is your branch for v1.1, to be released today. Your branch for changes on future releases (but not on v1.1) is **master branch**.

Other branches such as **v1.0-no-az-changes** and **v1.0-service_access-#144322245** are being used to PR corrections/edits back into 1.0 docs.

The **master branch** is in use for v1.2 development.

A **v1.1-branch** was created (using **master branch** as a snapshot) on 7/6/17.

The above info about branches comes from Megan Moore and is correct as of July 7, 2017.

## Staging

The staging docs are on PWS using https://docs-pcf-staging.cfapps.io/.

## Developing docs locally

This will make the book available at localhost:4567 and automatically update when you write changes to disk

```
cd book
bookbinder watch
```

## Pushing docs to CF

These docs are served as an app in CF

```
cd book
bundle install
bookbinder bind local
cd final_app
cf push p-cloudcache-docs-staging -b https://github.com/cloudfoundry/ruby-buildpack#v1.6.28
```

## Building Docs as part of docs-book-pcfservices

1. Clone `pivotal-cf/docs-book-pcfservices` into `~/workspace` directory
2. Clone this repo into `~/workspace` directory as well.
3. Edit the `docs-book-pcfservices/config.yml` to add:
 
    ```
    - repository:
        name: pivotal-cf/docs-cloud-cache     # name of our docs repo
        at_path: content                      # subfolder in our repo containing our erbs and images
      directory: p-cloud-cache                # url for our docs to live in, in html site
      subnav_template: cloudcache_subnav.erb  # name of file containing our navigation (appears to left of docs)
    ```
4. Edit the `docs-book-pcfservices/master-middleman/source/index.html.erb` to add, at the top of the `Pivotal Software` section:

    ```
    <li class="panel span3">
      <a class="configure" href="/p-cloud-cache/index.html" id="cloudcache">
        <div class="prodname">
          Pivotal <br>Cloud Cache
        </div>
      </a>
    </li>
    ```
5. Copy the `docs-cloud-cache/master-middleman/source/subnavs/cloudcache_subnav.erb` to `docs-book-pcfservices/master-middleman/source/subnavs/`
6. In `docs-book-pcfservices`, run `bookbinder watch` (after getting ruby/rbenv/bundle/etc installed)


