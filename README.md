# react-testing-jest

basic matchers::
1. .not.toBeNull()
2. .toHaveLength(2)
3. .toBe("12:00");
4. .toEqual("13:00")


case 1:
++++++
When an array is received in props and .map operation is performed::

export const AppointmentsDayView = ({appointments}) => 
(
<div id="appointmentsDayView">
    <ol>
    {appointments.map((appointment) => (
        <li key={appointment.startsAt}>
            {appointmentTimeOfDay(appointment.startsAt)}
        </li>
    ))}
    </ol>
</div>
)

each test file should have an import of react and reactdom:
import React from "react";
import ReactDOM from "react-dom";

describe('AppointmentsDayView', () => {
    let container;

    beforeEach(() => {
    container = document.createElement('div');
    });
     const render = component => ReactDOM.render(component, container);
     
     it('renders multiple appointments in an ol/li element', () => {
        // put the sample array as::
         const today = new Date();
        const appointments = [
            { startsAt: today.setHours(12, 0) },
            { startsAt: today.setHours(13, 0) }
        ];
        render(<AppointmentsDayView appointments={appointments} />);
        
        //basic tests
        expect(container.querySelector('div#appointmentsDayView')).not.toBeNull(); // check for parent div with some ids presence.
        expect(container.querySelector('ol')).not.toBeNull(); //check presence of ul element by queryselector
        expect(container.querySelector('ol').children).toHaveLength(2); // check ol's children
        
        //check for "li" element by querySelectorAll
        expect(container.querySelectorAll("li")).toHaveLength(2); // check for length
        // check for each li elements content
        expect(container.querySelectorAll("li")[0].textContent).toBe("12:00"); // check for each zeroth li elements content
        expect(container.querySelectorAll('li')[1].textContent).toEqual("13:00"); // check for each first li elements content
        
        expect(container.querySelectorAll('li > button')[0].type).toEqual('button'); //check for buttons type attribute
     });
    
    
 });

