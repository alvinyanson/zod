# Zod Keypoints


### Object Schema

Create an object schema

    const PersonSchema = z.object({
        name: z.string()
    });


Parse the passed object if it's valid or not (will throw error when parse failed)

    const parsedData = PersonSchema.parse(data);


Safe parse to handle error later

    const parsedData = PersonSchema.safeParse(data);




### Object with Array Schema

Create an object schema

    const StarWarsPersonSchema = z.object({
        name: z.string(),
    });


Create an object with array schema

    const StarWarsPeopleResultsSchema = z.object({
        results: z.array(StarWarsPersonSchema),
    });

Usage

    const parsedData = StarWarsPeopleResultsSchema.parse(data);


The `parsedData` is of type 

    const parsedData: {
        results: {
            name: string;
        }[];
    }


### Create type

    type Person = z.infer<typeof StarWarsPersonSchema>


### Simple validation

    const Form = z.object({
        name: z.string().min(1),
        phoneNumber: z.string().min(5).max(20).optional(),
        email: z.string().email(),
        website: z.string().url().optional(),
    });

Usage

    export const validateFormInput = (values: unknown) => {
        const parsedData = Form.parse(values);

        return parsedData;
    };