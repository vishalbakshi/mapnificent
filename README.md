# 30x30: Visualizing Rapid Network Service

This is the launchpad for building upon the proof of concept established during the SF DataJAM @ Code For America on Saturday, April 13, 2019.

DataJAM Outcome: <a href="https://docs.google.com/presentation/d/1Pm0a0NYYYtsFItfxuugKelZlJt3Z6Wwoy1wJS2nyM7E/edit?usp=sharing">Google Slides</a>

## Resources

- Mapnificent binary generator:https://github.com/mapnificent/mapnificent_generator
    - **Note: if you are converting the GTFS folder to binary using go, do not convert the GTFS folder to .zip**
        - ```go run mapnificent.go -d ~/gtfs/ -o bayarea.bin -v```
- Remix/Partridge (GTFS reader): https://github.com/remix/partridge
- GTFS data: https://transitfeeds.com/p/sfmta
- Adding mapnificent cities (in order to understand what goes into Mapnificent's data conversions): https://github.com/mapnificent/mapnificent_cities/tree/6363f4297febcb4e6bfe6544f577833d05e88564

## Brainstorm

The following points oultine the different tasks/features that can be pursued for future development of this project.

What is the purpose of this tool?

- A tool where you can propose a Rapid transit route using GTFS and see the impact in a way that’s digestible by all stakeholders	
    - Precedent: https://www.mapnificent.net/sanfrancisco/#12/37.7100/-122.3664/1860/37.7730/-122.4031
    - Goals:
        - Change the data the Mapnificent frontend is receiving:
            - By adding new R routes
            - By removing existing R routes
        - In order to show:
            - Impacted area (different colors)
            - Impacted time (difference in areas)
        - Understand how the data is structured
            - https://github.com/mapnificent/mapnificent_cities/tree/6363f4297febcb4e6bfe6544f577833d05e88564
            - Questions to ask:
                    - What is the existing state?
                    - What is the impact of 30x30?
                    - What are the public comments?
- No matter what tool or feature you develop, first consider:
    - How is GTFS structured as it exists (static and realtime)
    - How would GTFS be structured to show future/predictive data
- Potential tasks to explore when adding features
    - Update the GTFS file, (i.e.remove Rapid routes, remove walking radii, etc.)
    - Run Mapnificent locally and feed the frontend new data
        - Refer to: https://github.com/mapnificent/mapnificent_generator
        - **Note: if you are converting the GTFS folder to binary using go, do not convert the GTFS folder to .zip**
            - ```go run mapnificent.go -d ~/gtfs/ -o bayarea.bin -v```
    - How will this new data (positively or negatively) the success of the 30x30 initiative?
    - How can we incorporate public feedback?
        - Example: http://www.letsbikeoakland.com/survey/#/
    - What are relevant precedents to 30x30 to consider/study?
        - Van Ness Improvement Project
            - https://www.sfmta.com/projects/van-ness-improvement-project
        - Geary Project
            - https://www.sfmta.com/projects/geary-boulevard-improvement-project
        - Underground M
            - https://www.sfmta.com/blog/subway-sfsu-our-plan-take-m-line-down-under
- Further questions to explore:
    - What are the impacts of public comments on the feasibility of 30x30 based on their area/neighborhood of interest?
    - How can we use this data and its visualization to communicate pros/cons of transit changes to those affected by those lines (residents, business, etc.)?
    - Are there other apps/forms that can plug into this larger visualization tool (this will expand the community input from other sources (in-person discussions, twitter, etc.))
    - Comparisons of theoretical transit performance vs actual transit performance
        - What are the discrepancies between the two?
        - Schedule GTFS vs realtime GTFS
        - Refer to: https://transitfeeds.com/l/68-san-francisco-ca-usa
    - How do we toggle 30x30 treatments in the visualization?
        - How can we translate these treatments to existing transit improvement realities/methodologies (SFMTA manual, construction techniques/costs, etc.)
            - e.g. this route takes 40 minutes, but with 30x30 treatments it takes 20 minutes!
            - Example: https://www.sfmta.com/projects/muni-forward
            - TTRP: Travel Time Reduction Proposals
            - How can the user toggle different modes of transportation in the visualization?
            - MUNI, car, bike, BART, walk
            - Where/how will these features be built? What data do we have? What data would be needed?






# Mapnificent

Install [bower](http://bower.io/) and [jekyll](http://jekyllrb.com/).

    # You need node and npm
    npm install -g bower
    # You need ruby and bundler
    bundle install

Then get the cities data:

    git submodule init
    git submodule update

Then run:

    bower install
    jekyll serve -w


## How to add a city

In order to add a transit system to Mapnificent, [GTFS data](https://developers.google.com/transit/gtfs/) for that transit system needs to be available without charge under a license that allows its use with Mapnificent. If you find data for a city that is not on Mapnificent, [please follow the steps outlined in the Mapnificent City repository.](https://github.com/mapnificent/mapnificent_cities/blob/master/README.md)
