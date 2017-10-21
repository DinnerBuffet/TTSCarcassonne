# Tile Data

Each tile should have a script including variables needed to represent the information on the tile. The data format is as follows:
*In all examples, the "starting piece" is used*
*It should be noted that the "top" and "topleft" is from the perspective of the white player. All of the tiles are, in actuality, rotated by 180 degrees, which is taken into account in code with TILE_STANDARD_ROTATION
Data Format:
 sides - table of strings ( ie. {'City', 'Road', 'Field', 'Road'} ) Specifies the feature on each side of the tile, starting from the "top" clockwise (top is arbitrary, but must be consistent amoung pieces)
            features: 'City', 'Road', 'Field', 'River', 'Abbey'
 (optional) linkedQuadrants - table of tables of ints ( ie. {{2, 4}} ) Each table specifies which features are linked together, starting from the "top" at 1 and increasing clockwise.
            This only applies for features that take the middle of the side (ie. roads, rivers)
            In the example, the right side is linked to the left side (the road)
 (optional) linkedOctants - table of tables of ints ( ie. {{5, 6}, {7, 12}, {8, 9, 10, 11}} ) Each table specifies which half of each quadrant is linked to others, starting from the "topleft" at 5 and increasing clockwise.
            This is necessary for fields and cities, in particular, since both halves of a quadrant aren't always linked to each other.
            Also, this specifies how the fields on each half of a road feature are linked to other fields. Therefore, each road quadrant may also have 2 corresponding octants specified for that same side.
            In the example, the topleft and topright octants are linked
                            the righttop and lefttop octants are linked (This is the field on the top half of the road)
                            the rightbottom, bottomright, bottomleft, and leftbottom octants are linked (this is the field on the bottom half of the road)
 (optional) specialFeatures - table of tables containing a string (which specifies the feature), (optional) table of ints, and (optional) table of exactly 2 floats ( ie. {{'City-Field', {5, 6, 7, 12}, nil}} )
            The table of ints specifies what quadrants or octants this feature is linked to (if any).
            The table of floats specifies the relative x and z coordinates of the feature on this piece (if a figure can be placed on the feature).
            features:
                 Base features ('City', 'Road', 'Field', 'Abbey') - this allows for additional locations for specifying the base features.
                      this is useful for defining additional snap points, as well as allowing features which aren't connected to any quadrant or octant (there are a few fields like this).
                 'Cloister' = cloister - specifies the location of a cloister. Links are not used for this feature.
                 'City-Field' = city-field link - if the cities specified are completed, they score points to the specified fields. Multiple different cities and fields specified
                            are NOT linked to each other, only fields are linked to cities (and vice versa, in the case of using old rules (TODO: implement later?). Coordinates are not used for this feature.
                 'Road Intersection' = links roads to each other or other features. This is used for wagons.
                 Linked Features with no coordinates: 'Coat of Arms', 'Inn', 'Cathedral', 'Princess'
                 Unlinked Features of the tile: 'Volcano', 'Dragon', 'Hill'
                 'Garden' - specifies the location of a garden. Links are not used for this feature.